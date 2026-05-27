# SKILL: Gated Decision Pipeline Workspace Builder

## Description
Builds a customized top-of-funnel triage workspace by asking diagnostic questions about how a team sees and triages inbound items, then assembling a folder structure, stage contracts, and config files based on the answers.

## When to Use
When a team sees far more items, requests, or cases than it can pursue and wants to apply its decision criteria consistently and fast — reaching a defensible advance/decline on each, and handing advanced items cleanly to whatever committed effort sits downstream.

## Process

### Phase 1: Diagnosis (ask before building)

> **Org facts are already captured.** Run Setup wrote the organization's name, domain, systems of record, team, and voice to `_shared-config/` (org-profile.md and voice-and-tone.md). Read those first. Do NOT re-ask org-level facts — confirm them if needed. Ask only the workflow-specific questions below. If `_shared-config/org-profile.md` does not exist yet, the team skipped orientation; capture the basics first, then continue.

> **Learnings compound.** Before asking diagnostic questions, read `_shared-config/learnings.md`, but only `## General` and `## gated-decision-pipeline`. Apply reusable rules. Ignore task history.

Ask the following questions one at a time. Wait for each answer before proceeding.

**Question 1: What inbound items do you see, and from where?**
"Roughly how many items cross your desk, and through what channels — referrals, inbound forms, a queue, relationships? Where does the volume come from?"

**Question 2: What is the bar an item must clear?**
"What do you actually take on — type, scope, size, profile? Just as important: what is an automatic no, regardless of how strong the rest looks?"

**Question 3: What are your stages, and what is the go/no-go decision at each gate?**
"Walk me through what happens when an item arrives. Who looks at it, what do they check, how long does it take, and what does a 'no' look like at each gate?"

**Question 4: What rough check do you run before committing real effort?**
"Before advancing an item, what quick assessment do you run, and on what assumptions? Where do those reference figures or standards come from?"

**Question 5: What happens to an advance, and to a decline?**
"When you decide to advance, where does it go and what does the next owner need? When you decline, is the reason recorded anywhere?"

### Phase 2: Assembly

Based on the answers, build the workspace:

1. Start from the template: copy the matching architecture (`architectures/gated-decision-pipeline/` before finalize, `_kit/architectures/gated-decision-pipeline/` after) as your starting point into `workspaces/<name>/` (the team's live workspaces live there; rename <name> for the queue/cycle) — its CLAUDE.md, CONTEXT.md, stage CONTEXT.md contracts, and _config/ files are drafts to customize, not blank files to write from scratch (copy the folder contents, not any .DS_Store). Then adapt the structure to their answers. The default is three stages (intake, evaluate, decide), matched to their described gates; keep _config/ for the criteria and the bar, and _references/ for the decline log and comparables.
2. Write CLAUDE.md as the entry point: what this workspace is, current state, the structure map, and how to use it. Emphasize "decline fast" and that advanced items hand off to the downstream workspace.
3. Write CONTEXT.md as the routing file: the stage map, how stages connect, the advance→downstream handoff (build it to the handoff-brief schema in Constraint 08) and decline→_references log, and the AI-vs-Platform table.
4. Customize each stage's CONTEXT.md from the template's contract, using their process description — adjust the existing contract, do not write a new one from scratch.
5. Create config templates: decision-criteria.md, thresholds.md (automatic disqualifiers + weighing rules + a decline-reason taxonomy), evaluation-assumptions.md (rough, dated). Populate from their answers.
6. Set up _references/ with the decline log structure.
7. Flag what you could not confirm. Populate _config/before-you-trust-this.md: list every value you could not get directly from the team — especially compliance language, numeric thresholds, and rosters — mark each `[NEEDS CONFIRMATION — <owner>]`, name who signs off, and never invent these silently. Use `[TBD]` for values simply awaiting real data. (Constraint 08.)
8. Demonstrate one stage end to end. Run the first stage against a real or sample input and check the output against its "Done Looks Like" line and the `hiring-pipeline` worked sample (`architectures/_examples/hiring-pipeline/`). If there is no live input yet (a brand-new queue with no item in hand), use a sample item as the stand-in run, and mark the workspace "stands up now, activates on first inbound item."

### Phase 3: Orientation

After building, walk the user through:
- "Here is what I built and why each piece exists."
- "The point is speed: spend the least effort to reach a defensible decline, so attention goes to the items that fit. Evaluate against the bar in _config, not the requester's framing."
- "The rough check is a filter, not the full analysis. The real work lives downstream. Never let a screen-stage figure masquerade as the full analysis (Constraint 09)."
- "Every decline is logged with a reason. That keeps decisions consistent and, over time, shows you your own rejection patterns."
- "The first thing to populate is the bar — a sharp bar is what makes triage fast."

## Important Notes
- Do not build before completing the diagnosis. The questions are the skill.
- Keep it lean. The most common mistake is over-building a process whose entire value is speed. If they have fewer than three real steps, do not force three stages.
- Load and name the constraints this workflow uses: the universal 06 (Layer Triage) and 09 (Platform Boundary), plus 02 (Output Drift) so every evaluation comes out comparable, and 08 (Handoff Readiness) so an advance hands off cleanly. Pull 10 (Source Provenance) when items arrive as unvetted source sets. Pull 01 (AI Writing Patterns) if a stage drafts a memo or written rationale.
- Always annotate files with their ICM layer (L0–L4) so the user understands the architecture, not just the files.
