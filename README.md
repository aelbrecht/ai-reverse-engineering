# Reverse engineering project harness

The setup and orchestration used for the Fire Emblem Awakening reconstruction,
adapted for a fresh project. It retains the Nintendo 3DS research workflow,
native C++23/macOS target, model roles, connected ownership, verification rules
and evidence discipline.

This is a documentation scaffold. It contains no game source, ROMs, extracted
assets, research dumps, tools, build system, agent configuration or FEA Git history.
Azahar, Ghidra and the original verification runner are not included. Instructions
describe how to work; tooling must be supplied or built for the new project.

## Layout

```text
project-harness/
├── AGENTS.md                 Workspace and ROM-analysis instructions
├── README.md                 Adoption and starting prompts
├── examples/                 Worked contracts, handoffs and verification
├── native/
│   ├── AGENTS.md             Implementation, delegation and verification rules
│   ├── README.md             Future application's introduction
│   ├── WORKSPACE.md          Target, local entrypoints and active handoff
│   └── docs/
│       ├── ROADMAP.md         Scope and acceptance template
│       ├── KNOWN_BUGS.md      Deferred defects template
│       └── research/
│           └── README.md      Evidence-note format
└── work/                     Created locally; ignored generated data
```

The two instruction files closely follow the original workspace. Live game-specific
status, active handoffs and local paths have been removed from the templates.
Separately labeled examples retain selected FEA findings and historical results.
Format-specific behavior must be established from the new target's evidence.

## Worked examples

See [the reference examples](examples/README.md) for a process-lifecycle contract,
a scoped agent assignment and return handoff, and verification/report acceptance.
They show the expected level of detail without adding implementation or tooling.

## Start a project

1. For a new game, place a clean copy of these documentation files in a
   separate workspace named for the target. Open its root so both instruction
   levels are available. When a session starts directly in `native/`, also read
   the parent `AGENTS.md`. The template repository itself tracks files at its
   root; do not initialize a nested repository inside a template checkout.
2. Fill the target fields in [native/WORKSPACE.md](native/WORKSPACE.md). Keep the
   C++23/macOS and Nintendo 3DS assumptions unless intentionally choosing a
   different target; update both instruction files if those constraints change.
3. Supply the original image and research tools locally. Inspect installed tools
   and image metadata before extraction. Record paths in WORKSPACE.md and image
   identity/provenance in research; generated outputs belong in `work/`.
4. Keep the Sol/Terra/Astra roles in [native/AGENTS.md](native/AGENTS.md) when those
   models are available. Model names here are inherited project preferences;
   this scaffold does not configure or enable agents. If unavailable, agree an
   available mapping before delegating, preserving the same ownership boundaries.
5. Select and size the first milestone in [the roadmap](native/docs/ROADMAP.md).
   Add source, build files and verification tools only as the selected work needs
   them. The scaffold itself has nothing to compile or execute.
6. In the separate game workspace, initialize its repository in `native/`
   when version control is wanted. Configure your own signing identity and game
   remote; the template remote is for scaffold maintenance. Record the game
   project's commit/push permissions in WORKSPACE.md once supplied.

`AGENTS.md` is recognized by Codex; the workspace and roadmap files are project
conventions linked from those instructions. See the
[official workflow documentation](https://developers.openai.com/cookbook/examples/codex/iterating-development-workflows-with-codex).

## Starting prompts

For initial inspection, supply the game name and local image path with:

> Read AGENTS.md, native/AGENTS.md, native/WORKSPACE.md and native/docs/ROADMAP.md.
> Inspect the workspace, installed tools and supplied image headers without
> modifying the original image. Establish the executable identity, container
> layout and extraction prerequisites. Record reproducible evidence under work/
> and curate the relevant findings in native/docs/research/. Define a bounded
> first milestone with observable acceptance. Stop after that inspection and plan.

For an agreed milestone, replace `MS<number>` with its actual ID:

> Read the applicable instructions, workspace handoff and MS<number> in the
> roadmap. Audit its connected dependencies, then complete its implementation
> and acceptance within the authorized scope. Delegate independent outcomes under
> the ownership rules. Use only verification commands that actually exist; report
> missing tooling and unverified behavior. Update maintained claims and leave a
> concise handoff if work remains. Stop at this milestone's boundary.

To resume an interrupted milestone:

> Resume MS<number> from WORKSPACE.md and the roadmap. Reconcile the current
> source, evidence, live processes and build ownership before editing or running
> checks. Reuse valid results while their inputs remain unchanged. Continue to
> the existing acceptance boundary and report remaining gaps plainly.

## Sharing

Share the [template repository](https://github.com/aelbrecht/ai-reverse-engineering)
or a clean source archive before adding local inputs. The repository tracks only
the listed Markdown files and ignore rules. Create `work/` locally when needed;
empty directories are not tracked by Git. Keep original images, generated data,
credentials and tool checkouts out of later packages. Existing repository
changes travel through an authorized Git remote; never copy `.git` directories
or bundle repository metadata.
