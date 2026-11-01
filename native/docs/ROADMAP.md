# Roadmap

The goal is a faithful, source-built native C++23 reconstruction of the selected
game. This file owns priorities, milestone scope and acceptance. Research owns
source contracts; [known bugs](KNOWN_BUGS.md) owns defect details and reproductions.
Superseded plans and implementation chronology belong in Git history.

## Current status

No game has been selected and no implementation or verification is complete.
The milestone below is an unstarted example to adapt after initial inspection.
It is not evidence, a completed checkpoint or authorization to run a full roadmap.

## Initial milestone example

### MS1 — Image identity and executable landmarks

**Status:** proposed; select the target and confirm scope before execution.

**Dependencies:** a locally supplied original image; access to any required local
extraction and analysis tools. Inspect installed capabilities before adding tools.

- [ ] **1.1** Establish image identity, container sections, encryption/compression
  flags, bounds and relevant checksums without modifying the original.
- [ ] **1.2** Extract the admitted executable/data sections under `../work/` using
  metadata-derived offsets and verify their sizes and identities.
- [ ] **1.3** Identify one connected executable entry and its direct/indirect
  dependencies. Validate callback registration pointers where relevant.
- [ ] **1.4** Record the established behavior, unresolved branches and observable
  acceptance for a first native translation.

**Acceptance:** reproducible extraction and curated landmark evidence identify
the exact source image and executable, mappings, verified properties and unknowns.
Static analysis is not native execution or gameplay acceptance. No application,
emulation or broad function translation is part of this milestone.

**Completion:** not started. Add the bounded outcome, implementation revision and
actual report/evidence references only after verification.

## Subsequent milestones

Add milestones when the target and dependencies are known. Trace connected owners
and prerequisites before sizing them. Each milestone should fit a focused owner
session and a few coherent commits, with observable behavior at its boundary.

Keep the same structure: stable ID and outcome, dependencies, bounded subtasks,
acceptance and completion evidence. Define the actual source entry/callers,
branches, lifetime transitions and required native consumers. State imported or
controlled state and what remains unverified. A helper or next unsupported guard
alone is not a completed user outcome.

Name clean development/sanitizer and optimized application integration gates
when those builds exist. Routine commits need affected checks, not automatic
full playthroughs. Full route acceptance must cover its complete lifecycle;
performance work must preserve behavior, cadence and checks.

Retain accepted IDs and provenance. Split substantial unstarted outcomes using
unused IDs and carry unmet requirements forward. Check off work only after its
stated verification passes. Stop at the user's requested boundary.
