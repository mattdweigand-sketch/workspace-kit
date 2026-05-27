# Kit — Setup & Build Engine

## What This File Is

You are an AI agent. This file is the **setup engine** for the Kit. It runs the
organization's one-time orientation, builds workspaces, keeps the operating-system map current, and
(when the organization is ready) finalizes the repository into the organization's own AI operating
system.

You did not start here. `AGENTS.md` is canonical. Codex and other AGENTS-aware tools read it
directly. Claude Code auto-loads `CLAUDE.md`, which is only a thin wrapper that imports
`AGENTS.md`. From here on, this file is the machinery; `AGENTS.md` is the artifact.

Read this file first, then navigate to the specific files each step calls for. Do not load
everything at once. That is the whole point of the toolkit.

This repository is the Kit, a general-purpose system for putting AI behind the recurring
knowledge work any organization runs — a SaaS company, a professional-services firm, an agency, an
in-house team. It is deliberately industry-neutral: rather than ship a fixed catalog of named
workflows, it ships the four structural *shapes* that nearly all recurring knowledge work takes,
plus worked examples from different industries so you can see a finished one. It has three parts:

- **architectures/** — four reference workspace shapes (gated-decision-pipeline,
  recurring-operations-queue, recurring-document-production, learning-loop), each a working folder
  structure with its own `CLAUDE.md`, `CONTEXT.md`, and stage contracts. `architectures/_examples/`
  holds cross-industry worked instances (a hiring pipeline, a support-escalation queue, a monthly
  board report, a sales win/loss review) so you can study finished output, not just empty shapes.
  You copy and customize a shape to build the user's workspace.
- **constraints/** — ten reference files, each solving a specific problem teams hit when working
  with AI. You load these selectively, matched to the shape being built.
- **skill-starters/** — builder skills, one per shape plus a `build-from-scratch` meta-builder.
  Each runs a diagnostic interview, then assembles a workspace from the answers. These do the
  actual building.

> **Where the toolkit lives.** Before the organization finalizes, these three folders and this
> `SETUP.md` sit at the repo root. After finalize, they move together into `_kit/` and this
> file becomes `_kit/SETUP.md`. Everything in this file works in both states; where a path
> differs, it is called out as "root before finalize, `_kit/` after."

## A Note on Context Layers (ICM)

The architectures and builders tag every file with a context layer (L0–L4) under the
Interpreted Context Methodology (ICM). The layer says *when* a file loads: L0 the
always-loaded map (`AGENTS.md` at the root, `CLAUDE.md` inside legacy workspace templates),
L1 routing (`CONTEXT.md`), L2 the per-task stage contract,
L3 reference the model should follow (voice, standards), and L4 working files the model
should transform (source data, drafts). The discipline is to load only what a step needs, and
to keep "rules to follow" (L3) distinct from "content to transform" (L4) so the model does
not confuse the two. Constraint 03 (Context Hygiene) defines the full model — read it before
you start stamping layer tags on the files you build.

The word *layer* shows up in two unrelated ways across this toolkit; keep them separate.
**Context layers (L0–L4)**, the subject of this note, describe *when* a file loads. **Solution
layers (60/30/10)**, named in the constraint routing table below, describe *what kind of tool*
should solve a problem — traditional software, a rule-based system, or a language model. Same
word, different question.

## Context Matrix

The matrix below is the load contract for setup. It says what to read for each shape, and at what
depth, before a builder starts asking diagnostic questions. It complements the context-layer tags:
ICM says *when* a file loads; this matrix says *how much* shared context a builder needs.

Load levels:
- **full:** read the whole file.
- **summary:** use only the relevant digest or top-line facts.
- **section:** read only the named section.
- **pointer:** know the file exists; open it only when the builder or current answer requires it.
- **writes:** the builder creates or updates this file.
- **none:** do not load.

| Shape | `_shared-config/org-profile.md` | `_shared-config/voice-and-tone.md` | `_shared-config/learnings.md` | Constraints | Architecture | Builder |
|---|---|---|---|---|---|---|
| `gated-decision-pipeline` | full | summary | `## General`, `## gated-decision-pipeline` | routed list | pointer | full |
| `recurring-operations-queue` | full | full when responses leave the team | `## General`, `## recurring-operations-queue` | routed list | pointer | full |
| `recurring-document-production` | full | full | `## General`, `## recurring-document-production` | routed list | pointer | full |
| `learning-loop` | full | summary | `## General`, `## learning-loop` | routed list | pointer | full |
| `build-from-scratch` | full | full when writing | `## General`, `## build-from-scratch` | routed list | none | full |

Load only what the matrix names. Do not open every constraint, every architecture, or all of
`_shared-config/` because it feels safer. If a build truly needs extra context, say why, then load
the smallest file or section that answers the question.

## Run Setup / Add a Workflow

This is the entry point. When the user says **"Run setup"**, **"add a workflow"**, **"build a
&lt;workflow&gt;"**, or opens a session with no specific task, do this first:

1. **Check whether the organization has been set up before** — does
   `_shared-config/setup-progress.md` exist? That file is written at the end of the first setup;
   its existence is the hard signal that setup has already run. (Do not judge by placeholder text —
   key off the file.)
   - **No (first-time setup):** run **Organization Orientation** (below), then **The Onboarding
     Sequence** to build the first workspace, then write `_shared-config/setup-progress.md`
     recording what was built, then run **After First Setup: Write the OS Map** to turn the root
     `AGENTS.md` into the organization's operating-system map.
   - **Yes (returning):** read `_shared-config/org-profile.md` and
     `_shared-config/setup-progress.md`, greet the organization by name, summarize what has been
     built, and offer to add another workflow, set up another instance of one already built, update
     shared config, or resume an unfinished one. Do **not** re-run orientation. "Run setup,"
     "add a workflow," and "build a &lt;workflow&gt;" are all the same add-a-workflow intent on
     this path. After the build, run **Keeping the OS Map Current**.
2. Always ask before building, and stop with a working, populated workspace the organization can use.

Do not make onboarding feel like a form. Ask one question at a time, skip anything already answered
in a prior response, and acknowledge the skip briefly so the user knows you heard it. When the
user's answer clearly maps to a shape, recommend that shape and explain why. Show the full shape
menu only if the user asks for it or the mapping is genuinely ambiguous.

### Organization Orientation (first run only)

Before building any workflow, capture the organization once. Ask these one at a time, then write the
answers into `_shared-config/org-profile.md` and seed `_shared-config/voice-and-tone.md`. Both
files ship as placeholder templates (bracketed prompts); overwrite the placeholders with the
organization's real values rather than appending alongside them:

1. **What is the organization, and what does it do?** Name, what it does, who it serves, and the
   recurring work it wants to put behind AI, at a high level.
2. **What are your systems of record?** Where the authoritative data lives — the CRM, the
   accounting/ERP/finance platform, the ticketing or project tracker, the data warehouse, the
   HRIS/ATS. This is the platform boundary: what AI will narrate but never compute or override
   (Constraint 09).
3. **Who is on the team, and who owns what?** The roles that own the work, the data, and the
   sign-off, so workspaces route handoffs and approvals correctly.
4. **How does the organization sound in writing?** A first pass at the voice (how it addresses
   customers or partners, how direct it is about bad news, what it never sounds like). Seed
   `_shared-config/voice-and-tone.md`; it is fully refined the first time a writing workspace is
   built.

Orientation is org-level and runs once. Every builder reads `_shared-config/` and does not
re-ask these facts.

## The Onboarding Sequence

Run these steps in order. Each one names the file to read or run next.

1. **Route the work.** The organization itself is already captured in `_shared-config/` (from
   Organization Orientation). Ask only what work the user wants to run with AI, and map their answer
   to one of the four shapes using the routing table below. If they name more than one, handle the
   highest-priority workflow first and return for the others. Do not build them all at once.

2. **Pick the skill-starter.** Check the **Context Matrix** for the shape, then open the matching
   builder in `skill-starters/` (root before finalize, `_kit/skill-starters/` after). It is the
   instruction set for the build. Do not improvise a workspace; the builder's diagnostic questions
   are the work. Load only the org profile, voice, learnings, constraints, and architecture files
   named by the matrix and routing table.

3. **Run the diagnostic interview.** Ask the builder's questions one at a time. Wait for each
   answer. The answers become the content of the workspace. Do not skip ahead to assembly.

4. **Load the constraints this workflow needs.** Before assembling, read the constraint files
   named for this shape in the constraint routing table below. They shape the stage contracts and
   the `_config` files you are about to write. Load only those. Loading all ten is the
   context-hygiene mistake the toolkit exists to prevent.

5. **Instantiate the workspace.** Copy the matching shape — `architectures/<shape>/` before
   finalize, `_kit/architectures/<shape>/` after — into `workspaces/<name>/` (rename it for the
   user's actual workflow), and follow the builder's assembly phase to write `CLAUDE.md`,
   `CONTEXT.md`, the stage contracts, and the `_config` files from the interview answers. Copying
   never consumes the template, so a shape can be built any number of times. The reference shape's
   own files show you the target form, and the nearest worked example in `architectures/_examples/`
   shows you a finished one. (Live workspaces live under `workspaces/`; the organization's shared
   config lives in `_shared-config/`.)

6. **Populate `_config` with real values.** Pull org facts and the org voice from
   `_shared-config/` rather than re-asking; fill the workspace's remaining `_config` files with
   workflow-specific rules, the register overlay, terms, and constraints. A workspace with empty
   `_config` is a template, not an operating system. Help them fill at least the required files
   before you call onboarding done.

7. **Verify.** Run the Onboarding Complete checklist below. Report each item as pass or open.
   Do not declare onboarding complete while any item is open.

## Diagnose → Route

Most recurring knowledge work takes one of four structural *shapes*. Do not classify the user's
work by its industry or topic — classify it by its shape. Match the user's primary work to a shape
and run its builder. (Builder paths are under `skill-starters/` before finalize,
`_kit/skill-starters/` after.)

| If the work is shaped like… | Shape | Builder to run |
|---|---|---|
| Advancing one item through sequential go/no-go stages toward a terminal decision or action (a candidate through hiring, an opportunity through a sales pipeline, a loan application through approval, a project to launch) | gated-decision-pipeline | `skill-starters/gated-decision-pipeline-builder.md` |
| The same *type* of request arriving over and over: intake → process → deliver (support escalations, vendor onboarding, access requests, a content-request queue) | recurring-operations-queue | `skill-starters/recurring-operations-queue-builder.md` |
| Producing a document from numbers or facts you do not invent, on a cycle: verified data → drafted narrative → distribution (a monthly board report, a customer QBR, a status update, an investor or partner update) | recurring-document-production | `skill-starters/recurring-document-production-builder.md` |
| Making a repeated activity compound: capture an outcome → analyze why → write to a store → read it back next time (win/loss reviews, incident retrospectives, experiment post-mortems) | learning-loop | `skill-starters/learning-loop-builder.md` |
| The work fits no shape cleanly, or is a one-time serious deliverable from a messy source set | (build from the meta-pattern) | `skill-starters/build-from-scratch.md` |

If the user is unsure which they need, or wants to know where AI belongs at all before building
anything, start them with **Constraint 06 (Layer Triage)** and **Constraint 09 (Platform
Boundary)**. Those two answer "what should AI do, and what should my platform own" before a single
folder is created.

Platform-governed transactions — payments, payroll, order processing, record-of-truth writes — are
deliberately not a shape. They belong on the system that owns them (your accounting platform, your
ERP, your CRM), with its access controls and audit trail, not in an AI workspace. Do not build a
workspace to process them. AI's role around these events is the language and the judgment on top of
the platform: drafting the notice from platform-verified figures (document production) or fielding
the questions they generate (operations queue). See Constraint 09.

### Matching the shape, in practice

- **A single request can span two shapes.** For example, "monitor our SLA metrics and produce the
  monthly customer health report, and decide which accounts to escalate to a save play" is recurring
  document production (the report) *and* a gated decision pipeline (the save play). When a request
  decomposes like this, build the highest-priority shape first and return for the second — do not
  silently drop the half that did not fit the first shape you reached for.
- **Apply the platform-boundary filter first (Constraint 09).** If an enterprise platform already
  owns the workflow — CRM, ticketing, accounting, ATS — do not rebuild it. Build the
  language-and-judgment layer that rides on top of it.
- **If the work maps to no shape at all,** build a new workspace from the meta-pattern using
  **Constraint 06 (Layer Triage)**, **Constraint 03 (Context Hygiene)**, **Constraint 08 (Handoff
  Readiness)**, and **Constraint 09 (Platform Boundary)** as the recipe. `build-from-scratch.md` is
  the assembly guide. Still pull the constraints the nearest shape would load, by analogy — a
  partner-facing compliance document inherits **02 (Output Drift)** and **10 (Source Provenance)**
  for the same reasons the document-production shape does. Match the constraints to the shape you
  are closest to, not just to the fallback floor.

## Constraint Routing

Load the constraints named for the shape you are building. Read them before assembly, and name them
in the workspace `CLAUDE.md` so the user's team can find them later. Do not load the whole library.
(Constraint files are under `constraints/` before finalize, `_kit/constraints/` after.)

| Shape | Load these constraints | Why |
|---|---|---|
| **All workflows** | 06 (Layer Triage), 09 (Platform Boundary) | Decide what is AI vs. deterministic vs. platform before building. Roughly 60% traditional, 30% rule-based, 10% AI. |
| **gated-decision-pipeline** | + 02 (Output Drift), 08 (Handoff Readiness); 10 (Source Provenance) when items arrive as an unvetted source set; 01 (AI Writing Patterns) when a stage drafts a memo or recommendation | Decisions must be comparable item to item; the item hands off cleanly at the terminal stage; opportunities often arrive as messy source sets. |
| **recurring-operations-queue** | + 02 (Output Drift), 04 (Session Consistency); 05 (Voice Architecture) when responses are customer- or partner-facing | Each request must be handled consistently across many responders and on-voice when it leaves the building. |
| **recurring-document-production** | + 01 (AI Writing Patterns), 02 (Output Drift), 05 (Voice Architecture), 10 (Source Provenance) | The document must read clean, sound like the organization, stay consistent cycle to cycle, and tie every figure to a verified source. |
| **learning-loop** | + 04 (Session Consistency), 03 (Context Hygiene), 08 (Handoff Readiness); 10 (Source Provenance) when records ingest sourced data | Records must be comparable to aggregate into the store (04, load-bearing); the store stays clean and handoff-readable (03, 08); a stated-vs-assessed-reason check keeps spin and false precedent out of it (10). |
| **Scaling any workflow** | + 07 (Scaling vs. Automating) | When the same workflow runs many times, decide what to template vs. automate. |
| **Context degrading mid-build** | + 03 (Context Hygiene) | If your own context gets noisy during a long onboarding, this is the fix. |
| **Ingesting a data room or unvetted source set** | + 10 (Source Provenance) | Inventory and rank inputs before any stage drafts. AI flags provenance, duplicates, and conflicts; the platform owns the figures. |

## Onboarding Complete

Onboarding is done when every item below is true. Report each as pass or open.

- [ ] **Workflow identified.** The user confirmed which shape they are building and what their
      workflow is.
- [ ] **Workspace instantiated.** The shape was copied and renamed; it has a `CLAUDE.md`, a
      `CONTEXT.md`, and a `CONTEXT.md` for every processing stage. (A raw input-drop folder such as a
      `00_sources/` intentionally has none.)
- [ ] **`_config` populated.** The required reference files hold the user's real values, not
      placeholder text. Any value the organization did not supply is flagged, not invented: use
      `[NEEDS CONFIRMATION — <owner>]` for high-stakes values (legal/compliance language, financial
      thresholds, rosters) and `[TBD]` for data not yet available. See Constraint 08.
- [ ] **High-stakes values gated.** `_config/before-you-trust-this.md` lists every
      `[NEEDS CONFIRMATION]` value with its owner and status. Nothing customer- or public-facing
      ships until the high-stakes rows are cleared. (Constraint 08 defines the convention.)
- [ ] **Constraints loaded and named.** The constraints from the routing table were read, and
      the workspace `CLAUDE.md` names which ones apply.
- [ ] **One stage run end to end.** At least one stage produced real output, checked against
      its "Done Looks Like" line. Compare it to the nearest worked example in
      `architectures/_examples/` to see what finished output looks like. If there is no live input
      yet (a learning loop with no resolved record, a brand-new cycle), the matching worked example
      is the stand-in run, and the workspace is marked "stands up now, activates on first
      &lt;decision / cycle / request&gt;."
- [ ] **Handoff-ready.** A new team member could open the workspace folder and understand it
      without you in the room (Constraint 08 is the test for this).

If any box is open, return to the step that produces it. A half-built workspace handed off as
"done" is the failure mode this checklist exists to prevent.

## After a Build

Ask: "Anything about this workflow setup that should be remembered for next time?"

If yes, write the reusable rule to `_shared-config/learnings.md` under the matching shape section.
If the lesson applies across shapes, write it under `## General`. Do not write task logs here. Good
entries name the date, the reusable rule, and the evidence for it. Bad entries merely say what was
built.

## Registry Reconciliation

Before adding or modifying a shape or builder, compare:
- `architectures/<shape>/`
- `skill-starters/<shape>-builder.md`
- `skill-starters/build-from-scratch.md`
- the Diagnose -> Route table
- the Constraint Routing table
- the README shape list

If a shape exists on disk but is missing from the tables, add it silently and report what changed.

If a shape is listed in the tables but missing on disk, stop and ask before removing it from docs.

## After First Setup: Write the OS Map

At the end of the **first** setup — after the first workspace is built and
`_shared-config/setup-progress.md` is written — overwrite the root `AGENTS.md` with the
operating-system map below. `AGENTS.md` is canonical. `CLAUDE.md` stays a thin Claude Code wrapper
that imports `AGENTS.md`; do not duplicate project instructions there. This is the content
metamorphosis: the canonical instruction file stops being a toolkit bootstrap and becomes the
organization's own OS map. It is safe and automatic — nothing of value is lost, because the
machinery already lives here in `SETUP.md`.

Fill the parametric fields from the organization's files:
- `{ORG_NAME}` — from `_shared-config/org-profile.md`.
- `{KIT_POINTER}` — `SETUP.md` before finalize, `_kit/SETUP.md` after. (At first-setup time it
  is always `SETUP.md`; the finalize step updates it.)
- `{KIT_LOCATION}` — a bare phrase naming where the toolkit currently lives: before finalize,
  `the repo root` (the kit folders and `SETUP.md` sit at the top level); after finalize, `` `_kit/` ``.
  It appears in **two** places in the template below; fill both with the same value.
- `{BUILT_LIST}` — one line per workspace in `_shared-config/setup-progress.md`.
- `{AVAILABLE_LIST}` — the shapes not yet built (you can always build more instances of any shape).

Write exactly this structure (substituting the fields):

```markdown
# {ORG_NAME} — AI Operating System

`AGENTS.md` is canonical. Codex and other AGENTS-aware tools read it directly. Claude Code reads
it through the thin `CLAUDE.md` wrapper. Do not duplicate project instructions in `CLAUDE.md`.

This repository is {ORG_NAME}'s operating system for working with AI. It was set up from the
Kit, and it keeps growing: you can add workflows at any time. The toolkit machinery —
the setup engine and the library of workflow shapes — lives at {KIT_LOCATION} and runs whenever
you add or change a workflow.

## How this repository is organized
- `_shared-config/` — the organization, captured once: `org-profile.md`, `voice-and-tone.md`, and
  `learnings.md`. Every workspace reads these by contract. This is the org-level context that is
  true regardless of workflow.
- `workspaces/` — your live workspaces. Each has its own `CLAUDE.md` that maps it; open the
  workspace folder and read that file to work in it.
- The toolkit, at {KIT_LOCATION} — the setup engine (`SETUP.md`) and the workflow library
  (`architectures/`, `constraints/`, `skill-starters/`). You rarely open these directly; you
  reach them by saying "add a workflow."

## Workspaces built
{BUILT_LIST}

## Add a workflow

This operating system is not finished — it grows with the organization. To add a new workflow, set
up another instance of one you already run, or stand up any toolkit shape you have not built yet,
just say **"Run setup"**, **"add a workflow"**, or **"build a &lt;workflow&gt;"**. That routes to
{KIT_POINTER}, which runs the build.

Building *copies* a shape into a new `workspaces/<name>/`; it never consumes the template. So
every shape stays available forever, and you can build the same shape more than once (for example,
a second gated-decision-pipeline for a different process — just give it a distinct name).

Shapes still available to build:
{AVAILABLE_LIST}

## Working in a workspace

To use a workspace that already exists, open its folder and read its `CLAUDE.md` — that file is
the map for that workspace. `AGENTS.md` is the map for the organization.

## A note on the `L0`–`L4` tags you'll see
Files across the workspaces are tagged with a context layer, which just says *when* the file is
meant to be read: **L0** the always-on map (`AGENTS.md` at the root), **L1** the workflow router (`CONTEXT.md`),
**L2** a single step's instructions (a stage `CONTEXT.md`), **L3** reference the model follows
(voice, rules, schemas), **L4** the working files it transforms (source data, drafts). You do not
have to manage these; they are there so each step loads only what it needs.
```

### `_shared-config/setup-progress.md` template

Write this file at the end of the first setup, and keep it in sync with the OS map on every later
build (the two must always agree). Use exactly this structure so it stays consistent across sessions:

```markdown
# Setup Progress — {ORG_NAME}

Records what has been built from the Kit. The existence of this file is the signal that
first-time setup has already run. This file and the OS-map `AGENTS.md` must always agree.

## Organization
- {ORG_NAME} — {one-line description}. Orientation completed: {YYYY-MM-DD}.

## Workspaces built
| # | Workspace | Shape | Built | State |
|---|---|---|---|---|
| 1 | `workspaces/{name}/` | {shape} | {YYYY-MM-DD} | {one-line state} |

## Shapes still available to build
{comma-separated list of the four shapes not yet built; you can always build more instances of any}

## Finalized
{Omit until finalize runs. Then add one dated line per finalize/restore event.}
```

After writing the OS map, tell the user setup is complete and that they can keep building any
time by saying "add a workflow." Mention finalize as an optional, reversible tidy-up step they
can run whenever they want the repo root to read purely as their operating system.

## Keeping the OS Map Current

After **every** subsequent build (on the returning path), refresh the root `AGENTS.md`:
- Add the new workspace to the **Workspaces built** list (`{BUILT_LIST}`).
- Remove that shape from **Shapes still available to build** (`{AVAILABLE_LIST}`) the *first* time
  that shape is built, and never re-add it. Building a second instance of an already-built shape
  therefore does not change the available list — you can always build more instances regardless of
  what that list shows.
- Leave `{KIT_POINTER}` and `{KIT_LOCATION}` set to wherever the kit currently lives (`SETUP.md`
  / the repo root before finalize, `_kit/SETUP.md` / `_kit/` after).

Also append the new workspace to `_shared-config/setup-progress.md`. The OS map and
setup-progress.md must always agree on what has been built.

## Finalize (make this your operating system)

Finalize is an **explicit, reversible** step the organization runs when it wants the repo root to
read purely as its operating system, with the toolkit tucked out of the way. It is a near-pure
folder move — by this point `AGENTS.md` is already the OS map, so only its toolkit paths change.
`CLAUDE.md` remains the wrapper.

Run finalize **only when the user explicitly asks** ("finalize," "make this our operating system,"
"tuck the toolkit away"). Never finalize automatically, and never finalize the source toolkit repo
— only an organization's own working copy.

Steps:
1. Create `_kit/` at the repo root.
2. Move the toolkit into it: `SETUP.md`, `architectures/`, `constraints/`, and `skill-starters/`
   all move into `_kit/`. (This file becomes `_kit/SETUP.md`.) Do **not** move `_shared-config/`,
   `workspaces/`, `AGENTS.md`, `CLAUDE.md`, `README.md`, or `LICENSE` — those stay at the root.
3. Update the OS-map `AGENTS.md`: change `{KIT_POINTER}` from `SETUP.md` to `_kit/SETUP.md`, and
   change **both occurrences** of `{KIT_LOCATION}` from `the repo root` to `` `_kit/` ``.
4. Write `_kit/RESTORE.md` from the template below.
5. Update `README.md`: anywhere it locates the toolkit folders (`architectures/`, `constraints/`,
   `skill-starters/`) at the repo root, note they now live under `_kit/`. A standing parenthetical
   is enough — the goal is that a reader following `README.md` after finalize looks in the right
   place. (Restore reverses this.)
6. Record the finalize in `_shared-config/setup-progress.md` (a dated "Finalized" line).

After finalize, the organization keeps building exactly as before — "add a workflow" now routes to
`_kit/SETUP.md`, and builders copy from `_kit/architectures/`. Nothing about ongoing building
changes except the path the kit lives at.

### `_kit/RESTORE.md` template

Write exactly this when finalizing:

```markdown
# RESTORE — reverse the finalize step

This repository was finalized: the Kit was moved from the repo root into `_kit/` so the
root reads as the organization's operating system. This file reverses that move.

## What finalize did
- Moved `SETUP.md`, `architectures/`, `constraints/`, and `skill-starters/` into `_kit/`.
- Updated `AGENTS.md` (the OS map) so "add a workflow" points to `_kit/SETUP.md`.
- Left `CLAUDE.md` as a thin Claude Code wrapper that imports `AGENTS.md`.
- Noted in `README.md` that the toolkit folders now live under `_kit/`.
- Recorded the finalize in `_shared-config/setup-progress.md`.

## To restore the original root layout
1. Move the four items back to the repo root:
   `mv _kit/SETUP.md _kit/architectures _kit/constraints _kit/skill-starters .`
2. In `AGENTS.md`, change the kit pointer from `_kit/SETUP.md` back to `SETUP.md`, and change
   both kit-location mentions from `_kit/` back to `the repo root`.
3. In `README.md`, remove the `_kit/` note so it again locates the toolkit at the repo root.
4. Note the reversal in `_shared-config/setup-progress.md`.
5. Delete the now-empty `_kit/` and this file.

Nothing in `_shared-config/` or `workspaces/` moves during finalize or restore — your org config
and live workspaces stay at the root throughout. Building still works in both layouts; only the
path the toolkit lives at changes.
```

## How the Three Parts Relate

The constraints are the principles. The architectures are worked examples of those principles
applied to a workflow shape. The skill-starters turn a shape into a customized workspace for one
organization. You move left to right: understand the constraint, study the shape, run the builder.
Each workspace, once built, is self-documenting — its own `CLAUDE.md` is the map for that workspace,
the same way the root `AGENTS.md` is the map for the organization.

A note on support-folder naming: every workspace has a `_config/` (the organization's own rules,
voice, and terms). The second support folder is named for the job that workspace does, not by
accident — `_references/` for cross-run knowledge (standards, prior records), `_prompts/` for
reusable prompt fragments, `_store/` for the accumulating memory of a learning-loop workspace (where
the store *is* the deliverable), and `_templates/` for reusable output patterns. The variation is
deliberate; match the folder to the work, not to a uniform name. Fully worked sample runs do not
live inside a built workspace — they ship centrally under `architectures/_examples/` (one per
shape) as read-only calibration references; point users there rather than copying a sample into
their workspace.
