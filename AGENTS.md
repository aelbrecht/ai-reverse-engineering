# Reverse engineering workspace

This workspace is for extracting and reverse engineering a locally supplied
Nintendo 3DS ROM. Azahar is the upstream reference for loading and decompression;
Ghidra provides disassembly and decompilation when supplied locally. Neither tool
is bundled. Record the selected game and image identity in native/WORKSPACE.md
and its linked research before game-specific analysis.

The target is a source-built native macOS prototype using reconstructed game
logic. The prototype must not execute the original ARM binary or depend on 3DS
CPU, GPU, or system-service emulation. Azahar remains development tooling.
This distribution repository tracks the complete scaffold at the workspace
root. It contains no game implementation. When adopting the documentation into
a separate game workspace, keep the C++23 project and its Git repository in
`native/`, with generated data in the workspace's `work/` directory. Do not
initialize a nested repository inside this template checkout.

## Working practices

- Be concise, direct, and technical. Inspect the workspace and relevant source
  before changing anything.
- Prefer targeted changes and existing architecture. Use clear names and strong
  typing; avoid unrelated refactors and unnecessary dependencies.
- Keep tooling runnable on macOS or Linux. Check installed tools and their version
  requirements before installing or recommending additional dependencies.
- Run the narrowest meaningful verification and report what was actually tested.
  Distinguish source inspection, isolated routine tests, and full application runs.
- Ask only when an assumption materially affects correctness. State limitations
  and unresolved risks plainly.
- Use GPT-6.1 Sol for orchestration, investigation, implementation and routine
  reviews. Use GPT-6.1 Terra for well-specified tasks with objective checks. Reserve
  Astra for difficult tasks or specific unresolved fidelity questions requiring
  deeper analysis, not default checkpoint reviews; follow the delegation and
  escalation guidance in `native/AGENTS.md`.

## ROM analysis

- Preserve the original ROM. Use `work/` for extracted files, generated analysis,
  and temporary harnesses; do not commit ROMs or generated dumps.
- Inspect container headers and encryption/compression flags before extraction.
  Derive section offsets and memory mappings from metadata rather than guesses.
- Verify relevant checksums, bounds, and decompressed sizes. Record provenance and
  reproducible commands with analysis artifacts, not in this file.
- Reuse Azahar's parsing and decompression routines where practical. Prefer a
  focused exporter over building the full emulator solely for extraction. Retain
  upstream license notices when reusing code.
- The Azahar checkout may be modified or used as a source of code for local
  experimental tooling. Keep generated work separate from the upstream source.
- Treat RomFS assets, the ExeFS executable, and whole-ROM compression as distinct
  concerns. Extraction does not produce decompiled source.
- Treat Ghidra pseudocode, inferred types, and assigned names as analysis results
  requiring validation, not as recovered original source or a rebuildable project.
- Prefer translating connected original functions and callback tables, preserving
  data and execution order. Replace platform dependencies at explicit boundaries;
  defer structural redesign until the translated behavior is verified.
- Automatic analysis can miss indirect script callbacks. Use verified registration
  pointers to seed function discovery and record evidence for recovered names.

## Repository and external tools

- Commit coherent increments and push to the configured remote when the project
  owner has authorized those actions. Authorization from the source project does
  not transfer with this scaffold. Never force-push or publish ROMs, extracted
  assets, or dumps. Deployment requires explicit authorization.
- Use appropriate non-sandboxed tools directly for Git, Docker, networking,
  external services, and repository-state operations when available.
- GPG-sign every commit with the configured default settings using non-sandboxed
  tools. Never bypass signing; resolve signing failures before committing.
- Transfer repository changes between machines through the configured Git remote
  using authorized pushes and clone/fetch/pull. Never use Git bundles, copy Git
  metadata, or edit it manually. Use destination-local, minimally scoped
  credentials; do not forward SSH/GPG agents or copy keys/tokens without an explicit
  request for that mechanism after explaining its risks. If remote access or
  publishing authorization is missing, stop that action and ask.
- Use public unauthenticated research or existing CLI/API/connector credentials.
  Never access signed-in website accounts or reuse browser credentials unless the
  user explicitly requests that website's UI for the task.
- Never host local projects through OpenAI Sites.

## Maintaining these instructions

Keep this file current when durable project instructions or practices change.
Consolidate and remove stale guidance instead of appending a running history.
Keep detailed paths, tool inventories, version snapshots, progress logs, and
analysis findings in their appropriate artifacts.
