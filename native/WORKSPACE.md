# Workspace

Agent-facing operational context. Read [AGENTS.md](AGENTS.md), the
[parent instructions](../AGENTS.md) and [ROADMAP.md](docs/ROADMAP.md) for practices,
scope and task selection. README.md owns visitor basics. This file maps layout,
maintained entrypoints and active handoffs; it is not an archive of old commands.

## Target

| Field | Current value |
| --- | --- |
| Game and edition | Not selected |
| Source platform | Nintendo 3DS |
| Runtime target | Native C++23 on macOS; no original ARM execution or 3DS emulation |
| Original image path | Not supplied |
| Image/executable identity and provenance | Not established; record in linked research |
| Azahar checkout | Not supplied |
| Ghidra installation/project | Not supplied |
| Agent roles | Sol owner; Terra bounded tasks; Astra difficult unresolved questions |
| Game repository and remote | Not configured; this checkout distributes the template |
| Commit/push authorization | Not supplied for the new project |
| Deployment authorization | Not supplied |

Paths are relative to the workspace where practical. Keep credentials out of this
file. Change target assumptions deliberately and update the instruction files to
match. Missing inputs block the actions that depend on them, not unrelated work.

## Layout

- This distribution repository tracks the scaffold from the workspace root.
  In a separate game workspace, `native/` is the game repository and its parent
  is the asset/research workspace. Do not nest repositories in this checkout.
- Future `src/`, `include/` and `tests/` own implementation, typed interfaces and checks.
- Future `tools/` owns reusable automation; [docs/research/](docs/research/README.md)
  owns original evidence and provenance.
- `../work/` holds ROM-derived assets, captures, generated reports, temporary
  harnesses and scratch notes outside Git.
- Local upstream tools remain outside the native runtime and repository.

Only Markdown and ignore files are supplied. The source, tools and test folders
above are intended locations, not existing implementation.

## Build and verification

No build system, presets, tests, application or verification runner exists yet.
There is no valid build or test command for this scaffold.

Once introduced, link the actual build manifests and shared runner here. Inspect
their current help/parsers and configuration for requirements, defaults and limits.
Keep one maintained build entrypoint; keep required checks and lease rules in
AGENTS.md. Record actual commands, source/binary/input identities and results with
generated reports. Do not substitute example commands for executed verification.

## Tooling and source evidence

Add entrypoints only after they exist. Link the extractor, analysis exports,
shared verification runner and relevant subsystem contracts as they are created.
Keep tool inventories and versions with the research they qualify. The active
milestone selects which evidence matters; avoid reading every note as onboarding.

## Handoff

No active task, build owner, verification process or acceptance report exists.
The next action is to establish the target and select a bounded milestone with
the project owner. The roadmap's example is not an instruction to begin analysis.

When a task is interrupted, replace this section with only its active milestone
and execution boundary, source state, live process/build ownership, completed
checks, unfinished verification and blocker or next action. Use precise evidence
references; clear the handoff once resolved. Detailed scratch notes stay in
`../work/` and durable findings move to their maintained research home.
