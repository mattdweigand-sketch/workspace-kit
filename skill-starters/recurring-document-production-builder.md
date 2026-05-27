# SKILL: Recurring Document Production Workspace Builder

## Description
Builds a customized document-production workspace by asking diagnostic questions about a team's recurring reader-facing communications, then assembling a folder structure, stage contracts, and config files based on the answers.

## When to Use
When you produce reader-facing communications on a recurring cycle (recurring reports, board reports, statements, scheduled notices) and want a structured, controlled process that keeps the numbers tied to source and the voice consistent.

## Process

### Phase 1: Diagnosis (ask before building)

> **Org facts are already captured.** Run Setup wrote the organization's name, domain, systems of record, team, and voice to `_shared-config/` (org-profile.md and voice-and-tone.md). Read those first. Do NOT re-ask org-level facts — confirm them if needed. Ask only the workflow-specific questions below. If `_shared-config/org-profile.md` does not exist yet, the team skipped orientation; capture the basics first, then continue.

> **Learnings compound.** Before asking diagnostic questions, read `_shared-config/learnings.md`, but only `## General` and `## recurring-document-production`. Apply reusable rules. Ignore task history.

Before creating any files, ask the user the following questions one at a time. Wait for each answer before proceeding.

**Question 1: What do you produce, on what cycle?**
"What reader-facing communications do you create on a recurring basis, and how often — a recurring report, a board report, statements, scheduled notices? List everything you send at least once a year, with its cadence."

**Question 2: Where do the numbers come from, and who verifies them?**
"Walk me through what happens between 'the period closed' and 'the report is sent.' Where do the numbers come from — the system of record, a data warehouse, source reports? Who reconciles them? Who drafts? Who reviews? Describe your actual process, not the ideal one."

**Question 3: Where does review and sign-off happen?**
"At which points do you stop and review before something reaches a reader? Is there a number-reconciliation check, a compliance or legal review, a manager sign-off? If review only happens at the end, that is useful to know."

**Question 4: What reference material stays the same across cycles?**
"What applies to every communication you send? The team's core voice is already in `_shared-config/voice-and-tone.md` — I only need the report register overlay (how a recurring report or notice differs from the team's standard voice). Beyond that: required disclosures and footers, cautionary language, format templates, per-report specifics. List what exists and where it lives, even if it is only in someone's head right now."

**Question 5: What does 'done' look like for your most common report?**
"For the communication you send most often, describe the final output. Format, length, the disclosures it carries, how it reaches the reader (portal, email). What makes it ready to send?"

### Phase 2: Assembly

Based on the answers, build the workspace:

1. Start from the template: copy the matching architecture (`architectures/recurring-document-production/` before finalize, `_kit/architectures/recurring-document-production/` after) as your starting point into `workspaces/<name>/` (the team's live workspaces live there; rename <name> for the report/cycle) — its CLAUDE.md, CONTEXT.md, stage CONTEXT.md contracts, _config/ files, and `_prompts/` fragments are drafts to customize against, not blank files to write from scratch (copy the folder contents, not any .DS_Store). The shape ships no inline `_example/`; the worked sample for this shape is `architectures/_examples/monthly-board-report/`, which you study as a calibration reference rather than copy into the workspace. Then match the structure to their process. The default is three stages (data, draft, distribution); keep _config/ for reference material and _prompts/ for the reusable cycle fragments (e.g., a standard variance-narrative or disclosure-check prompt). If compliance/legal review is a distinct gated step, add 02a_review.

2. Write CLAUDE.md as the workspace entry point. Include:
   - What this workspace is (based on their description)
   - Current state (new workspace, no active cycle)
   - Structure map (listing all folders and their purpose)
   - How to use (step-by-step based on their cycle)

3. Write CONTEXT.md as the routing file. Include:
   - Stage map table (stage name, purpose, inputs, output location)
   - How stages connect, emphasizing that the data stage gates the others
   - Reference material list

4. Customize each stage's CONTEXT.md from the template's contract (adjust the existing contract, do not rewrite from scratch). Include:
   - Purpose (derived from their process description)
   - Inputs (what this stage needs, referencing specific files)
   - Process (steps, based on their description)
   - Output format (based on their "done" description and format patterns)
   - "Done looks like" (one sentence)

5. Create config file templates:
   - voice-and-tone.md, format-patterns.md, constraints.md (use the three-file architecture from Constraint 05). The team's core voice already lives in `_shared-config/voice-and-tone.md` (from Run Setup) — reference it, do not redefine it; capture only this workflow's register overlay (how its deliverable differs from the team's standard voice).
   - If they mentioned per-report or per-reader specifics: create placeholders for each

6. Populate constraints.md with the starter constraints, including the report-specific ones (every figure ties to source, cautionary language present, required disclosures present) and ask the user to add their own and confirm with the right owner. Use the worked sample at `architectures/_examples/monthly-board-report/` (its metrics pack, draft, and final report) as the calibration target for how complete a finished cycle looks.
7. Flag what you could not confirm. Populate _config/before-you-trust-this.md: list every value you could not get directly from the team — above all the compliance and disclosure language (the footer, cautionary-statement rules, any reporting-standard handling) — mark each `[NEEDS CONFIRMATION — counsel/compliance]`, name who signs off, and never invent or soften these. Use `[TBD]` for values simply awaiting real data. (Constraint 08.)
8. Demonstrate one stage end to end. Run the data stage against a real or sample period and check the output against its "Done Looks Like" line and the `monthly-board-report` worked sample's metrics pack (`architectures/_examples/monthly-board-report/`). If there is no live cycle yet, use that worked sample as the calibration reference, and mark the workspace "stands up now, activates on the first reporting cycle."

### Phase 3: Orientation

After building, walk the user through:
- "Here is what I built and why each piece exists."
- "The data stage gates everything. No figure reaches a report until it ties to source. This is what keeps a wrong number out of a reader's inbox."
- "The constraint file has starter rules including disclosure and cautionary language. Read through them, confirm them with the right owner, then add your own."
- "The first thing to populate is [most impactful config file based on their answers]."

## Important Notes
- Do not build anything before completing the diagnosis. The questions are the skill.
- The data stage is the highest-value stage. A reporting process that drafts before the numbers are verified is how a restated figure reaches a reader. Emphasize the reconciliation gate even if their current process is looser.
- Compliance is a real constraint surface here, not a style preference. Where the user is unsure about disclosure or performance language, tell them to confirm with the right owner rather than guessing.
- If the user's process has fewer than 3 distinct steps, do not force more stages. Verify-then-send is valid if that is their actual workflow.
- Always annotate files with their ICM layer (L0–L4) so the user understands the architecture, not just the files.
- Load and name the constraints this workflow uses: 01 (AI Writing Patterns), 02 (Output Drift), 05 (Voice Architecture), and 10 (Source Provenance) when more than one version of an export or source report is in play, plus the universal 06 (Layer Triage) and 09 (Platform Boundary).
