# _shared-config — the organization, captured once

This folder holds the org-level configuration that every workspace shares. It is filled in **once**,
during Run Setup's orientation, and read by every builder and every workspace afterward — so the
organization's name, systems of record, team, and voice are stated in one place instead of
re-collected for each workflow.

## What lives here
- **`org-profile.md`** — the organization: what it does, its systems of record (the platform
  boundary), and its team/roles. Builders read this instead of re-asking org-level questions.
- **`voice-and-tone.md`** — the organization's core written voice (the "direction" file from
  Constraint 05). Every writing workspace references this for the core voice, then adds its own
  register on top (a customer email, a board report, and an internal brief differ in register, not
  in organizational voice).
- **`learnings.md`** — reusable corrections and preferences discovered while building or running
  workflows. Builders read `## General` plus their own shape section before asking diagnostic
  questions.
- **`setup-progress.md`** — created by Run Setup once the organization is onboarded: which
  workspaces have been built, when, and what is next. (Not present until the first setup runs.)

## How workspaces reference it
A workspace built under `workspaces/` reaches this folder by a stable relative path
(`../../_shared-config/...`). Each writing workspace's local voice file is a thin pointer to
`voice-and-tone.md` plus that workspace's register overlay — so updating the org voice once updates
every workspace. If a workspace is ever moved out of this repo, update its pointer to wherever the
organization keeps this shared config.

## How Run Setup uses it
The presence of `setup-progress.md` is how Run Setup distinguishes a first-time setup (orientate,
then build) from a returning one (greet, offer to add a workflow or update config). That file is
written at the end of the first setup, so its absence is the signal that setup has not run yet,
the same flag the canonical root `AGENTS.md` and `SETUP.md` key off. `CLAUDE.md` is only a Claude
Code wrapper that imports `AGENTS.md`.
