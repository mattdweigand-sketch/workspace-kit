# SKILL: Build From Scratch Workspace Builder

## Description
Builds a customized workspace for work that fits none of the four standard shapes — most often a single serious deliverable from a messy, unvetted source set (a memo, a one-time report, a case write-up, a one-off letter). Asks diagnostic questions about the deliverable, where the sources came from, and what the system of record is, then assembles an inventory → review → draft workspace tuned to the run.

## When to Use
This is the fallback. Reach for it when someone hands you a folder of files of unknown age and authority and needs one serious deliverable out of it, and the work maps to no recurring lifecycle stage and no standard shape. If the work clearly fits a shape, use that shape's builder instead (gated-decision-pipeline, recurring-operations-queue, recurring-document-production, learning-loop). If the same deliverable recurs on a cycle, use recurring-document-production. If the sources are already clean and inventoried, the inventory stage is light — but it still runs, because "the sources are clean" is itself a judgment a human should confirm, not assume.

## Process

### Phase 1: Diagnosis

> **Org facts are already captured.** Run Setup wrote the organization's name, domain, systems of record, team, and voice to `_shared-config/` (org-profile.md and voice-and-tone.md). Read those first. Do NOT re-ask org-level facts — confirm them if needed. Ask only the workflow-specific questions below. If `_shared-config/org-profile.md` does not exist yet, the team skipped orientation; capture the basics first, then continue.

> **Learnings compound.** Before asking diagnostic questions, read `_shared-config/learnings.md`, but only `## General` and `## build-from-scratch`. Apply reusable rules. Ignore task history.

Ask the following questions one at a time. Wait for each answer.

**Question 1: What is the deliverable?**
"What single artifact does this workspace produce — a memo, a recommendation, a case write-up, a one-time letter? Who reads it, what decision does it inform, and what does it have to accomplish to be good? Is there a format, length, or template it must follow?"

**Question 2: Where did the source set come from?**
"Where do the raw materials live, and how did they arrive — through a system with a document register and version history, or as a pile in a shared drive or an email thread? This matters: if a register already tracks versions and owners, that register is your inventory and the workspace reads it rather than rebuilding it. If it is an un-pruned pile, the inventory stage is doing real work."

**Question 3: What is your system of record for numbers?**
"Name the single authoritative source for figures — the platform export, the data warehouse, the executed agreement, the audited statement. This is the source the workspace is never allowed to adjudicate against or recompute. If you cannot name one for a given number, that ambiguity is the first thing the inventory will surface."

**Question 4: How messy is the source set, really?**
"How often do you get three versions of the same file, a transcript with two meetings in it, a deck that no longer matches reality? If the inputs are clean and controlled, the inventory is light. If they are a year of un-pruned drafts, the duplicate and version analysis is the highest-value part of the workspace. Tune the depth to the mess."

**Question 5: Is anything in the set sensitive?**
"Are there files that must be noted but never copied or quoted into summaries or the draft — personal data, privileged material, anything under NDA? The workspace will record their existence and structure only and never reproduce their contents."

**Question 6: Does anything carry across deliverables?**
"Is there house style, a prior comparable deliverable, or a standing standard the draft should follow? For a true one-off there often is not — the deliverable is grounded in its own sources. But if something reusable exists, it goes in _references/ rather than being re-derived."

### Phase 2: Assembly

Based on the answers:

1. Confirm the shape. The default is two stages (01_inventory, 02_draft) with a human review gate between them. Adjust only if an answer demands it:
   - If deciding what is even in scope is its own job (a very large set): add 01a_triage in front of the inventory.
   - If the deliverable must clear a compliance or legal pass before it ships (a regulated disclosure, an external letter): add 02a_review after the draft. Do not fold compliance into the draft stage.
   - Resist adding more. If the work needs many recurring stages, it is not a one-off — route it to the nearest standard shape instead.

2. Create the folder structure by hand — this fallback has no template shape to copy. Build it directly: `00_sources/`, the numbered stages each with an `output/`, `_config/`, and `_references/` — adding 01a_triage or 02a_review only if step 1 called for them. If the deliverable is close to one of the standard shapes, borrow that shape's stage-contract phrasing as a starting point rather than writing from a blank file.

3. Write CLAUDE.md:
   - What this workspace is (their deliverable, their source situation)
   - Structure map
   - How to use (drop sources into 00_sources/, inventory, review, draft — one deliverable, then done)
   - Key decisions (especially the review gate and the platform boundary, citing their system-of-record answer)

4. Write CONTEXT.md routing file:
   - Stage map with the review gate as the checkpoint between 01 and 02
   - How the stages connect, and why the order cannot reverse (you cannot cite a source ID the inventory has not assigned)
   - Reference material locations
   - The AI vs. Platform table, with their system of record named in the platform row

5. Write the stage contracts:
   - Inventory: the provenance pass tuned to their mess level (light if clean, deep duplicate/version analysis if not). If a document register exists, instruct it to read the register, not rebuild it. End the stage with the stop-and-hand-back review gate.
   - Draft: their deliverable's format from the spec, citing every claim to a source ID, labeling inferences, flagging unsupported claims, closing with Open Items and a Source Usage Map.

6. Populate _config:
   - deliverable-spec.md: filled from Question 1 (deliverable, audience, what it must accomplish, format, deadline, out of scope)
   - source-hierarchy.md: filled from Questions 2, 3, and 5 (system of record, the authority ladder as far as known, sensitive sources, where the sources came from)

7. If they named anything reusable in Question 6 — house style or voice is the usual one — create the file in _references/, or point to the shared reference library if one exists. The team's core voice already lives in `_shared-config/voice-and-tone.md` (from Run Setup) — reference it, do not redefine it; capture only this workflow's register overlay (how its deliverable differs from the team's standard voice). Otherwise leave the README note and keep _references/ empty; a one-off rarely needs more. A single standing reference like voice does not make this a recurring workflow.
8. Flag what you could not confirm. Populate _config/before-you-trust-this.md: list every value you could not get directly from the team — especially the system(s) of record for each figure class in source-hierarchy.md — mark each `[NEEDS CONFIRMATION — <owner>]`, name who signs off, and never invent these silently. Use `[TBD]` for values simply awaiting real data. (Constraint 08.)
9. Demonstrate the inventory stage. If the source set is already in 00_sources/, run the inventory and stop at the review gate, checking its output against the "Done Looks Like" line. If 00_sources/ is still empty at onboarding, walk the user through the inventory contract as the stand-in, and mark the workspace "stands up now, activates when the source set lands."

### Phase 3: Orientation

Walk the user through. Highlight:
- "The inventory stage stops before drafting and hands the room back to you. That pause is the whole point — review the authority ranking before anything gets written. The most important artifact in here is source_inventory.md, not the draft."
- "Drop your sources into 00_sources/. They get copied, never modified — they are the provenance anchor every citation points back to."
- "The draft cites every claim to a source ID and flags anything the sources do not support. If you see a NOT SUPPORTED flag, that is the workspace being honest, not failing — it is telling you where a human still needs to verify."
- "This is a unit of work, not infrastructure. When the deliverable ships, the workspace has done its job. If this kind of deliverable starts recurring, tell me — it has outgrown this fallback and belongs in a standard shape."

### Recommended Constraints

Load these constraint files, and name them in the workspace CLAUDE.md so the team can find them. Load the one a stage needs when that stage runs, not all of them at once. This fallback loads the meta-pattern (06, 03, 08, 09) plus whatever the nearest standard shape would load.

- **Constraint 10 (Source Provenance)** — the spine of this workspace. The inventory stage is this constraint given a folder structure: the inventory, the authority ladder, and the duplicate/conflict/missing-context logs are its four artifacts. Read it before building the inventory stage.
- **Constraint 06 (Layer Triage)** and **Constraint 09 (Platform Boundary)** — read first, with the user. They decide what AI does (inventorying, summarizing, surfacing conflicts, drafting), what a deterministic tool does (exact-duplicate hashing, the figures themselves), and what the platform owns (the system of record). The model narrates numbers; it never computes or blends them.
- **Constraint 03 (Context Hygiene)** and **Constraint 08 (Handoff Readiness)** — the meta-pattern for one-off work: keep the working context clean and leave the deliverable in a state a new owner could pick up.
- Plus whatever the nearest standard shape would load — e.g. if the deliverable is a written report, pull 01 (AI Writing Patterns) and 02 (Output Drift) the way recurring-document-production does.

## Important Notes
- Do not build before completing the diagnosis. The questions are the skill.
- The inventory stage is the highest-value stage in the workspace. If the user wants to skip straight to drafting because "the sources are fine," explain that a confidently wrong deliverable almost never comes from a bad prompt — it comes from a source set no one inspected. The inventory is cheap insurance against an expensive error.
- The review gate is not optional. Do not let the workspace draft from an unreviewed inventory. If the user will not review, at minimum surface that the draft rests on an uninspected source ranking.
- A one-off that keeps coming back is not a one-off. The first time the user copies this workspace for the third instance of the same deliverable, raise it: the work is recurring, and a standard shape will serve them better than rebuilding this by hand each time.
- This workspace prepares language and judgment, never figures. If the user expects it to calculate or reconcile a number, that is a platform job — point them at Constraint 09.
- Always annotate files with their ICM layer (L0–L4) so the user understands the architecture, not just the files.
