# SKILL: Learning Loop Workspace Builder

## Description
Builds a customized learning-loop workspace by asking diagnostic questions about how a team could capture and learn from why an outcome happened, then assembling a folder structure, stage contracts, config files, and a store based on the answers.

## When to Use
When a team wants its outcomes to compound — to systematically learn why it wins or loses, succeeds or fails, at a recurring kind of outcome and turn that into reusable intelligence — rather than relearning the same lessons one case at a time. This is a learning loop, not a pipeline or a tracking system; it explains *why* an outcome happened and remembers.

## Process

### Phase 1: Diagnosis (ask before building)

> **Org facts are already captured.** Run Setup wrote the organization's name, domain, systems of record, team, and voice to `_shared-config/` (org-profile.md and voice-and-tone.md). Read those first. Do NOT re-ask org-level facts — confirm them if needed. Ask only the workflow-specific questions below. If `_shared-config/org-profile.md` does not exist yet, the team skipped orientation; capture the basics first, then continue.

> **Learnings compound.** Before asking diagnostic questions, read `_shared-config/learnings.md`, but only `## General` and `## learning-loop`. Apply reusable rules. Ignore task history.

Ask the following questions one at a time. Wait for each answer before proceeding.

**Question 1: What outcome do you want to learn from, and how do you learn it resolved?**
"What recurring outcome do you want to understand — won/lost, succeeded/failed, kept/churned? How do you typically learn it resolved — a debrief, public record, the grapevine? This establishes the trigger and the resolution signal."

**Question 2: Where does the factual record and the comparison point live?**
"Where is the record of what we did — our offer, our entry, our terms — and where does the comparison point (the winning outcome, the benchmark) come from? Your system of record, relationships, public data? This is the governed source; the model must never invent it."

**Question 3: What actually decides your outcomes?**
"What dimensions decide the result — price, certainty/speed, structure, relationship, quality? This seeds both the canonical question bank and the decisive-dimension tag."

**Question 4: Which counterparties or intermediaries recur?**
"Who are the counterparties or intermediaries you encounter again and again? This becomes a controlled list — which ones you win through, and whose feedback proves reliable, are two of the highest-value patterns this store surfaces."

**Question 5: Who owns the 'why' call, and how skeptical are you of stated reasons (the stated-vs-actual-reason check)?**
"Who internally owns the final read on why we won or lost — the team lead, the owner? And how much do you trust a stated reason at face value? This sets the human-validation gate and how hard the workspace pushes on stated-vs-assessed reasons."

**Question 6: What would you change if you knew exactly why you win and lose?**
"If, across 50 cases, you knew exactly why you win and lose, what would you change — which cases you chase, how you compete, which relationships you build? This defines the payoff and who consumes the store."

### Phase 2: Assembly

Based on the answers, build the workspace:

1. Start from the template: copy the matching architecture (`architectures/learning-loop/` before finalize, `_kit/architectures/learning-loop/` after) as your starting point into `workspaces/<name>/` (the team's live workspaces live there; rename <name> for the loop) — its CLAUDE.md, CONTEXT.md, stage CONTEXT.md contracts, _config/ files, and _store/ (README + patterns.md scaffold) are drafts to customize against, not blank files to write from scratch (copy the folder contents, not any .DS_Store). The shape ships no inline `_example/`; the worked sample for this shape is `architectures/_examples/sales-win-loss/`, which you study as a calibration reference rather than copy into the workspace. Then adapt to their answers: three stages (signal, analysis, capture), plus _config/ and the _store/ folder with records/ and patterns.md. The _store/ is the deliverable — make it visible.
2. Write CLAUDE.md: what this is, the learning-loop shape and how it differs from a linear pipeline (the output feeds back into the store), current state, structure map, how to use. Call out the stated-reason guardrail in Key Decisions.
3. Write CONTEXT.md: the stage map, how the loop closes (capture writes the store; signal and analysis read it back), how the store feeds the decision and strategy workspaces, and the AI-vs-Platform table (the system of record and source data own what happened; the model proposes the why and keeps stated vs. assessed distinct; a human validates it).
4. Customize each stage's CONTEXT.md from the template's contract — adjust the existing contract, do not write a new one from scratch.
5. Create config templates: review-questions.md (the canonical set — the most important file, with the stated-vs-assessed question load-bearing), taxonomy.md (controlled tags including the controlled counterparty list), store-schema.md (record shape with our-position-vs-comparison-point and gap, patterns structure, privacy handling). Populate from their answers.
6. Set up _store/: keep the README, an empty append-only records/ folder, and the hypotheses-only patterns.md scaffold (0 records). Seed a few falsifiable hypotheses if useful, but mark them untested and do not let them drive strategy. See _store/README and the `sales-win-loss` worked sample's store (`architectures/_examples/sales-win-loss/_store/patterns.md`) for the shape.
7. Flag what you could not confirm. Populate _config/before-you-trust-this.md: list every value you could not get directly from the team — especially the controlled counterparty/intermediary list — mark each `[NEEDS CONFIRMATION — <owner>]`, name who signs off, and never invent these silently. Use `[TBD]` for values simply awaiting real data. (Constraint 08.)
8. Demonstrate one stage end to end. If an outcome has already resolved, run the signal stage on it and check the output against its "Done Looks Like" line. If none has resolved yet, point the user at the `sales-win-loss` worked sample (`architectures/_examples/sales-win-loss/`) as the calibration reference, and mark the workspace "stands up now, activates on the first resolved outcome."

### Phase 3: Orientation

After building, walk the user through:
- "Here is what I built and why each piece exists."
- "This is a loop, not a pipeline. The deliverable is the store, not any single write-up. Resist perfecting one record; invest in making records comparable so the corpus reveals patterns."
- "Comparability is the whole game — every analysis answers the same canonical questions in the same shape and uses the same taxonomy tags (Constraint 04). Changing the questions breaks comparability with prior records."
- "A stated 'why you lost' reason is often a polite fiction. The stated-vs-assessed question and the human validation gate are the defenses against capturing spin as fact and poisoning the store."
- "A human — the team lead / owner — validates the why before it is captured. A confident, wrong 'why' in the store skews future decisions."
- "Read patterns.md before the next case or before setting strategy — and feed it to your decision and strategy workspaces. That is the loop paying off."

## Important Notes
- Do not build before completing the diagnosis. The questions are the skill.
- The canonical review questions are the highest-value config. Spend the most time here; a loose or shifting question set makes the store un-aggregatable. The stated-vs-assessed reason question is load-bearing — do not drop it.
- The counterparty/intermediary list is a controlled list on purpose. Two of the most valuable patterns (which ones we win through, whose feedback proves reliable) require a stable vocabulary.
- This is sensitive intelligence — our own behavior, our gap to the comparison point, our read on named relationships. Address access and handling in store-schema.md.
- It does not replace the pipeline or the tracking system — it rides on them. The record of what happened is the platform's; this workspace adds the why and the memory. The loop is triggered by outcomes and pays back into strategy.
- Load and name the constraints this workflow uses: 04 (Session Consistency) — the load-bearing one, 03 (Context Hygiene), 08 (Handoff Readiness), plus the universal 06 (Layer Triage) and 09 (Platform Boundary). Pull 10 (Source Provenance) when records ingest sourced data and more than one version is in play.
- Always annotate files with their ICM layer (L0–L4); note that _store/ is an L3/L4 hybrid — the signature of the learning-loop shape.
