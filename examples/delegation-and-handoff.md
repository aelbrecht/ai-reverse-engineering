# A bounded assignment and return handoff

This is an illustrative task packet based on the [process contract](process-contract.md).
It is not a historical transcript or an active assignment. The paths below show
an example project layout; no corresponding source or tests ship in this scaffold.

## Assignment from the connected owner

**Owner:** Sol owns the scheduler, connected consumers, integration and the shared
build/verification lease. Terra owns the bounded regression fixture described
below. Sol has finished changing the relevant scheduler API before this task starts.

**Outcome:** add regression coverage that distinguishes child completion, parent
resumption and resource disposal under the established scheduler contract.

**Evidence:** use the process contract and its pinned P1 reference. Relevant
original routines are child insertion `0x00312b28` / `0x00303750`, End
`0x00312478`, update `0x00314f14`, and cleanup `0x00314e4c`. The fixture starts at
the native scheduler boundary; it does not establish original game bootstrap.

**Established behavior:** Call reloads and advances the current command after its
callback. A blocking child created by the callback can run later in the same
frame. End releases the block immediately. The parent's command traversal is not
revisited that frame, and child disposal occurs during the subsequent cleanup.

**Write boundary:** the example fixture file `native/tests/process_lifecycle.cpp`.
Read the existing scheduler and production constructors. Do not change scheduler
APIs, consumers or build configuration without returning the newly discovered
coupling to Sol. File separation alone does not make that API work independent.

**Acceptance:** inspect the callback sequence, command continuation, parent block
count and disposal boundary for each of these cases:

1. The child ends during its first update; parent resumption waits for its next visit.
2. Another blocking child remains; ending the first child does not resume the parent.
3. A Call callback changes its command pointer; automatic advancement uses the
   changed pointer rather than a cached pre-callback value.
4. Child disposal precedes parent disposal and disposed IDs are rejected.

**Execution boundary:** Terra may edit the agreed fixture. Sol retains the shared
build lease, so Terra does not run CMake, CTest or another verification process
against that shared build. A private build would require an explicitly independent
resource/output arrangement; it is not assumed merely because the files differ.

**Unresolved scope:** reparenting, original allocation limits, live cadence and
presentation behavior are not established by this assignment. Do not add guessed
behavior to make a fixture pass. Return a concrete discrepancy if the current API
cannot expose the required observations.

**Return:** identify changed files, implemented fixture cases, checks actually
executed, remaining gaps and any process/build ownership. Sol integrates, repairs
connected behavior, verifies acceptance and handles the authorized signed commit.

## Example return before owner verification

The following is a hypothetical response format, not a claim that these changes
or checks were performed:

> Changed `native/tests/process_lifecycle.cpp` for the four agreed cases. The
> fixtures use production process creation with explicit controlled starting state.
> They observe command order, block release and disposal separately.
>
> I reviewed the assertions against the supplied contract. Build and test execution
> are not performed: Sol still holds the shared build lease. The fixtures therefore
> remain unverified. No process was started and I hold no build lease.
>
> Sol's next action is to inspect the diff, build the affected target and run its
> exact registered cases through the existing project runner. No roadmap acceptance
> is claimed. Original runtime cadence and presentation remain outside this task.

The owner should replace hypothetical paths and execution instructions with real
entrypoints before dispatching this packet. If evidence conflicts or a fixture
reveals a fundamental ownership ambiguity, Sol investigates that question. Astra
is appropriate for a specific unresolved fidelity question, with competing
explanations and a minimal failing case; it is not a routine completion gate.
