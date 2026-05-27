# SKILL: Recurring Operations Queue Workspace Builder

## Description
Builds a customized request-handling workspace by asking diagnostic questions about the inbound requests a team fields between formal events, then assembling a folder structure, stage contracts, and config files based on the answers.

## When to Use
When a team handles a steady stream of ad hoc questions and soft requests and wants consistent, accurate, on-voice responses — with sensitive requests reliably escalated rather than answered casually.

## Process

### Phase 1: Diagnosis (ask before building)

> **Org facts are already captured.** Run Setup wrote the organization's name, domain, systems of record, team, and voice to `_shared-config/` (org-profile.md and voice-and-tone.md). Read those first. Do NOT re-ask org-level facts — confirm them if needed. Ask only the workflow-specific questions below. If `_shared-config/org-profile.md` does not exist yet, the team skipped orientation; capture the basics first, then continue.

> **Learnings compound.** Before asking diagnostic questions, read `_shared-config/learnings.md`, but only `## General` and `## recurring-operations-queue`. Apply reusable rules. Ignore task history.

Ask the following questions one at a time. Wait for each answer before proceeding.

**Question 1: What type of request arrives repeatedly?**
"What kinds of questions and requests come in — status checks, document re-sends, performance questions, change-of-scope interest, complaints? List the common ones."

**Question 2: How is a request handled today?**
"Walk me through what happens when one arrives. Who sees it, how fast does it get a response, and what do they check before replying?"

**Question 3: Where is the line between what the team answers and what gets referred?**
"What can the team answer directly, and what must go to a principal, compliance, or counsel? Who owns each kind of referral?"

**Question 4: Where do answers with numbers come from?**
"When a response includes a figure or status, where does that number come from? Is there a check that the requester is authorized to receive it?"

**Question 5: Do you keep a record or an FAQ?**
"Do you log answered requests, and do you have a set of vetted answers to the questions that recur?"

### Phase 2: Assembly

Based on the answers, build the workspace:

1. Start from the template: copy the matching architecture (`architectures/recurring-operations-queue/` before finalize, `_kit/architectures/recurring-operations-queue/` after) as your starting point into `workspaces/<name>/` (the team's live workspaces live there; rename <name> for the queue/cycle) — its CLAUDE.md, CONTEXT.md, stage CONTEXT.md contracts, _config/ files, and the four starter response templates in _templates/ are drafts to customize, not blank files to write from scratch (copy the folder contents, not any .DS_Store). Then adapt to their answers: three stages (intake, resolve, respond), plus _config/ and _templates/. If they verify requester identity, add an authentication step in or before intake.
2. Write CLAUDE.md: what this is (and that it is *not* transaction processing — anything that changes a balance, moves money, or alters an account is governed by the system of record, not an AI workspace; see Constraint 09), current state, structure map, how to use.
3. Write CONTEXT.md: the stage map, how stages connect, the escalation path, and the AI-vs-Platform table (the platform owns figures and the record; the model classifies, retrieves, and drafts; humans own anything that commits the organization).
4. Customize each stage's CONTEXT.md from the template's contract — adjust the existing contract, do not write a new one from scratch.
5. Create config templates: response-standards.md (service levels, voice, the answer-vs-refer line, never-do list), request-context.md (the working stakeholder record and routing map), faq-bank.md (the compounding vetted-answer store). Populate from their answers. The team's core voice already lives in `_shared-config/voice-and-tone.md` (from Run Setup) — reference it, do not redefine it; capture only this workflow's register overlay (how its responses differ from the team's standard voice).
6. Customize the four starter templates that ship in _templates/ (acknowledgment, resolution, holding-statement, escalation) to the team's voice and escalation rules; add a template for any other request type they handle repeatedly.
7. Flag what you could not confirm. Populate _config/before-you-trust-this.md: list every value you could not get directly from the team — above all the answer-vs-refer line and the authorized-contact roster in request-context.md (an unconfirmed roster blocks safe authentication) — mark each `[NEEDS CONFIRMATION — team lead/compliance]`, name who signs off, and never invent these silently. Use `[TBD]` for values simply awaiting real data. (Constraint 08.)
8. Demonstrate one stage end to end. Run the intake stage against a real or sample request and check the output against its "Done Looks Like" line and the `support-escalation-queue` worked sample (`architectures/_examples/support-escalation-queue/`). If there is no live request yet, use a sample request as the stand-in run, and mark the workspace "stands up now, activates on the first inbound request."

### Phase 3: Orientation

After building, walk the user through:
- "Here is what I built and why each piece exists."
- "Classification comes first, before anyone drafts. A departure signal that reads like a routine question is exactly the one this catches."
- "Every figure comes from the platform, never from the model's memory. A plausible number is a wrong number."
- "Escalation is a designed step. Sensitive requests get an acknowledgment and a routing, not an off-hand answer that commits the organization."
- "The FAQ bank compounds — the respond stage writes vetted answers back into it, so the same question stops being a research task and answers stay consistent across everyone who replies."

## Important Notes
- Do not build before completing the diagnosis. The questions are the skill.
- The answer-vs-refer line in response-standards.md is the highest-stakes config. Where the user is unsure, tell them to confirm with the right owner rather than guess.
- This is request traffic, not transactions. If they describe operations that change a balance or move money, those are governed by the system of record, not a workspace to build (Constraint 09).
- Load and name the constraints this workflow uses: the universal 06 (Layer Triage) and 09 (Platform Boundary), plus 02 (Output Drift) and 04 (Session Consistency). Pull 05 (Voice Architecture) when responses are customer-facing.
- Always annotate files with their ICM layer (L0–L4).
