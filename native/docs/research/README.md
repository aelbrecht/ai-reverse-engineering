# Research evidence

Curated findings belong here; generated extraction outputs, disassembly exports,
Ghidra projects, captures and logs belong under the workspace's `work/` directory.
No research has been established for a new target. The separate
[worked examples](../../../examples/README.md) summarize selected historical FEA
evidence; their findings do not transfer automatically to another game.

Give each connected subsystem one maintained evidence home. Record enough to
reproduce the finding and distinguish source facts, native policy and unknowns:

- Original image/executable identity, revision/region, addresses and memory mapping.
- Relevant functions, registration pointers, callers and consumers.
- Branches, return values, widths, wrapping, call/callback order and ownership.
- For scripts/processes: cursor advancement, child creation, continuation/wait
  behavior, completion and teardown.
- Extraction/analysis provenance, actual commands and tool versions where relevant.
- Observations and their domain: original execution, static instruction evidence,
  controlled native state, rendering/audio or isolated models.
- Native implementation references, performed checks and remaining discrepancies.

Treat decompiler output and inferred names/types as hypotheses until validated.
Asset identity does not establish execution, and equal final state does not prove
timing, callback or RNG order. Preserve uncertainty at the affected claim.

Link local generated evidence relative to each note. From this directory,
`../../../work/` is the generated workspace. Publicly shared notes should retain
useful provenance and reproduction steps even when their local artifacts are not
distributed. Do not include original binaries, asset dumps or credentials.
