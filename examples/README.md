# Worked reference examples

These examples show how the Fire Emblem Awakening workflow turns source evidence
into a contract, assigns bounded work and qualifies verification. Read the example
relevant to the current task; they are not additional onboarding requirements.

| Need | Example |
| --- | --- |
| Describe original behavior precisely enough to translate and test | [Process lifecycle contract](process-contract.md) |
| Delegate a bounded outcome and return useful context | [Assignment and handoff](delegation-and-handoff.md) |
| Understand runner responsibilities and record bounded acceptance | [Verification and acceptance](verification-and-acceptance.md) |

The process contract summarizes documented FEA research. The task packet and
return handoff are illustrative, not transcripts or active assignments. The
verification example contains selected fields from a real historical report and
a historical milestone record; neither establishes acceptance for this scaffold.

No game code, tools, raw disassembly, ROM-derived assets or complete generated
reports are supplied. Reuse the structure and precision. Establish another
target's behavior from its own evidence, and replace example paths with real
project entrypoints before assigning work.

## Source provenance

Sources were inspected in the FEA workspace on 2026-11-01. Paths below identify
the original materials; they are not files or executable entrypoints in this
repository. The content hashes identify the inspected versions without claiming
that a current source revision reproduces an old result.

| Reference | Original workspace path | Relevant content |
| --- | --- | --- |
| P1 | `native/docs/research/ms5-process-runtime.md` | Recovered structure; tick order and lifetimes; supported native commands |
| R1 | `native/docs/ROADMAP.md` | MS7 tutorial/battle coexistence and the MS6–MS8 acceptance record |
| V1 | `native/tools/verify_ms5_checkpoint.py` | `lease`, `run_checkpoint`, `verify_report`; schema 4 |
| H1 | `work/ms5/ms6-8-dev-20261028-e/report.json` | Historical schema-3 development preflight |

SHA-256 of each inspected source file:

```text
P1 d11805a67cd9fa004b0da720fa326ba050d7d3d8a13f622bf3468e6d081a1274
R1 8fed65894de9ab0e84cda0e7e46ea1bd6d4a4efa8323abf34f4402cb49af11cd
V1 a7822b81fafffce3fe4352a2e10cbcae92349fabf891012ae5b4525dc54e9028
H1 1d454a0ee2930db7d586981006f305d52c7cca2b5d6e5f4f0413e1afe8c05222
```

This addition inspected source documents, runner code and report metadata. It did
not repeat ARM analysis, execute the original game or rerun native verification.
The underlying research exports and historical artifacts remain outside this
repository, so these examples alone do not independently authenticate the findings.
