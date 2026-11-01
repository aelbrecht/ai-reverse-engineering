# Process completion and parent continuation

This is a worked summary of documented FEA behavior, not a universal scheduler
design. Source [P1](README.md#source-provenance) identifies European `CTR-P-AFEP`
and executable SHA-256
`9fd0afb613c35c3c104ae2d40d7666897243c7fb755520f04b067e097e2df7e1`.
Its evidence is ARM listings and Ghidra exports, not an observed gameplay trace.

## Behavior to preserve

A blocking child can finish and release its parent's block before its resources
are destroyed. The parent resumes only when traversal actually visits it again.
Collapsing completion, resumption and destruction into one operation changes order.

| Original routine | Documented responsibility |
| --- | --- |
| `0x00312b28`, `0x00303750` | Insert a child at the head, record its parent and optionally increment the parent's blocking-child count |
| `0x00312478` | Mark the process and descendants ended; release their parent blocks immediately |
| `0x00314f14` | Update traversal: older siblings, current process, then its current child head |
| `0x00100544` / `0x00314e4c` | Cleanup before the next update; children are disposed before their parent |
| `0x00314ecc` | Post-update traversal; ended processes do not receive ordinary post hooks |

The current process's command traversal happens before its children update. A
new child can therefore run in the same frame. If that child ends during its
update, unblocking does not revisit the parent's already traversed commands.

## Expected sequence for a controlled fixture

This is an expectation derived from the contract, not a captured trace or a test
result. Start with a runnable parent P and no other blockers or sleep delay. P's
current Call creates blocking child C; its following command records resumption.
C ends on its first update and creates no further children.

| Boundary | Required observation |
| --- | --- |
| P invokes Call | C is attached and P's blocking-child count increases |
| Call returns | P's current command is reloaded and advanced; the block prevents the following command from executing |
| Child traversal in the same frame | C runs and ends; P's block count decreases immediately |
| Remainder of that frame | P's resumption command has not run; C receives no ordinary post hook |
| Cleanup before the next update | C is disposed; its old process ID is stale |
| Next actual visit to P | Its following command can run once, if no other gate blocks it |

Checking only P's final block count would miss an early resumption or early
resource release. Check the intermediate boundaries and callback order.

## Callback semantics belong in the same contract

The original command forms differ even when they call the same native routine:

- **Call:** invoke, reload the current command pointer, advance and continue
  dispatch subject to the scheduler's gates. It is not a retry-until-zero Poll.
- **Poll:** a nonzero callback result yields; zero reloads and advances the
  command pointer and continues dispatch.
- **Repeat:** the callback owns advancement; ordinarily yield unless the
  continuation flag requests another dispatch in the same tick.

If a Call callback advances its own command pointer, Call's automatic advance
advances it again. If it selects a label, Call advances from the newly selected
location. A translation must inspect both the callback and its command-table
entry; identifying the called function alone is insufficient.

## Native boundary and limits

FEA uses native ownership and typed process IDs rather than original host-incompatible
member-function pointers. The contract preserves order and lifetime; it does not
require copying the ARM object layout into a host object.

Related checks should cover an additional blocker, a sleeping parent, stale IDs,
callback-modified command pointers and child-before-parent disposal. Keep each
fixture's starting state explicit. Passing them would establish only that native
behavior under those inputs. It would not establish full scene execution, original
frame timing or pixel/audio parity. Reparenting is outside P1's supported tree.
