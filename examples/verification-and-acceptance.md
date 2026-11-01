# Verification mechanics and bounded acceptance

This example explains the FEA runner and a real historical acceptance record.
It supplies no runner, report validator or executable commands for this scaffold.
Source references [V1, H1 and R1](README.md#source-provenance) identify the inspected
code, historical report and roadmap.

## What the runner actually does

The inspected runner's `run_checkpoint` holds a cooperative file lock while it
executes its plan and writes the final report. `lease` uses a nonblocking exclusive
lock and rejects another cooperating holder. An unrelated direct CMake invocation
does not automatically acquire that lock; the owner must keep it idle or put it
under the same ownership policy.

The run records its configuration, selection, Git state, source snapshot and
authenticated inputs. It checks source contents before executing steps, records
built/executed identities, checks input and binary identities at applicable stages,
and compares the final Git HEAD and source snapshot. Mutation invalidates a run;
assigning it a convenient revision afterward does not repair its evidence.

The report records Markdown guidance separately from runtime source inputs. A
documentation change is not silently relabeled as a runtime change, and runtime
changes cannot be hidden by calling them documentation.

The owner's workflow is:

1. Select the actual changed behavior and its registered checks. Freeze the
   relevant implementation, build and input state for the acceptance run.
2. Acquire the shared execution lease. Run affected CTests and selected positive
   scenarios; use private outputs/state for independent headless chains. Preserve
   dependencies within capture, replay and save/resume chains.
3. Wait for child processes to finish or be stopped, publish the report and release
   ownership. A second owner must not rebuild the shared binaries during a run.
4. Authenticate the completed report once with the runner's read-only verifier.
   The verifier reacquires its lease while checking artifacts. It never executes
   command strings from the report.
5. Interpret what the checks establish, then record the bounded outcome in the
   roadmap. A mechanically valid report does not by itself establish fidelity.

The inspected `verify_report` checks schema, successful status, declared scope,
configuration, source snapshots, input manifests, build/binary identities, CTest
inventory and artifacts, and the expected command plan and results. If supplied,
the expected report hash must match. Its authentication is consistency and identity
checking against the configured project and artifacts, not an independent gameplay
observation or a digital signature over the report.

## A real historical report excerpt

These fields are copied exactly from H1, a development preflight recorded for the
MS6–MS8 work. Other fields are deliberately omitted, so this is not a complete or
validatable report:

```json
{
  "schema": 3,
  "kind": "bounded-native-ms5-preflight",
  "status": "passed",
  "git_head": "5a29514654b642d35c68abdacde60590a70e380b",
  "git_head_after": "5a29514654b642d35c68abdacde60590a70e380b"
}
```

H1's declared selection uses the `dev` preset and selected menu, input, tutorial,
battle, dialogue/skip and tactical scenarios with their CTests. Its scope explicitly
excludes a full clean checkpoint and original-scene acceptance. `passed` applies
to that declared scope, not to the whole game.

The inspected V1 verifier requires schema **4**, so it rejects this schema-3 report
before full artifact checks. H1 remains a historical record. Do not edit its schema,
hashes or revision to make it appear current, and do not describe this excerpt as
freshly authenticated. A current claim needs a current compatible run and its
actual artifacts.

Git HEAD also does not identify all executed content when the working tree is
dirty. The source snapshots and recorded Git status qualify the execution state;
the later implementation commit and the report's recorded HEAD can legitimately
differ. Preserve that distinction in the completion record.

## What a bounded milestone completion looks like

R1 records **MS7, tutorial and battle coexistence**, as complete for an admitted
combination, with implementation `0fde01b` and verification in the combined MS6–MS8
source tree. Its recorded outcome is:

- Ordinary attack and return work with the tutorial present, absent or closing.
- Observer and GUI ownership remain balanced, and control returns to ordinary
  map input; input still blocks where the original behavior requires it.
- A repaired historical recording retains its input prefix and reaches map input
  at tick 2069, beyond the previous fault at tick 1711.

Those ticks describe the recorded native repair route. They do not establish
original-device timing or support for every tutorial/battle combination. The
completion combines a concrete user route, ownership constraints, a revision,
qualified verification and an explicit boundary. Copy that structure for a new
milestone; do not copy MS7's completed status into a new project's roadmap.

No build, gameplay replay or report reauthentication was performed while adding
this reference example. Only the pinned source material and report fields were
inspected.
