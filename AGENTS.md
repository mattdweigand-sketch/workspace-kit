# Kit

Shared project instructions for Kit.

`AGENTS.md` is canonical. Codex and other AGENTS-aware tools read it directly. Claude Code reads
it through the thin `CLAUDE.md` wrapper.

## What this project is

Kit is a plain-file toolkit for building AI operating systems around recurring knowledge work.
It is for teams that want controlled AI workflows for reports, request queues, decision pipelines,
and learning loops without replacing their systems of record.

## How to work in this repo

If `_shared-config/setup-progress.md` does not exist, setup has not run. Read `SETUP.md` and follow
it when the user says `Run setup`.

If `_shared-config/setup-progress.md` exists, setup has already run. Read `_shared-config/` and the
canonical root `AGENTS.md` operating map before adding or changing workflows.

When adding a workflow, route through `SETUP.md` before finalize and `_kit/SETUP.md` after finalize.
Do not load every architecture, constraint, or skill-starter at once.

## Project structure

- `SETUP.md` — setup engine for orientation, workflow builds, operating-map updates, and finalize.
- `architectures/` — reference workflow shapes and worked examples.
- `constraints/` — selective reference files for reliable AI workflow design.
- `skill-starters/` — builder instructions for each workflow shape.
- `_shared-config/` — organization-level config used after setup.
- `workspaces/` — live organization workflows created by setup.

## Conventions

- `AGENTS.md` is the only canonical root operating map. Update it, not `CLAUDE.md`.
- `CLAUDE.md` is only a Claude Code compatibility wrapper that imports `AGENTS.md`.
- Non-Claude agents should read `AGENTS.md` first.
- Setup and finalize must rewrite the root operating map in `AGENTS.md`.
- Load context selectively: root map first, routing file next, stage contract only for the active step.

## Do not do without asking

- Do not run finalize unless the user explicitly asks.
- Do not move toolkit folders into or out of `_kit/` without confirmation.
- Do not delete, overwrite, or reset live `workspaces/` or `_shared-config/` content.
- Do not write to external systems or send stakeholder-facing output without human review.

## Deeper context

- `SETUP.md` — read when running setup, adding a workflow, updating the operating map, or finalizing.
- `README.md` — read when updating user-facing startup instructions.
- `constraints/06-layer-triage.md` — read when deciding whether work belongs to AI, automation, or software.
- `constraints/09-platform-boundary.md` — read when separating AI work from systems of record.
