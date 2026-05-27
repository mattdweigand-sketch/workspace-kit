# Kit

For any organization that wants to build with AI instead of just use it. It turns your team's recurring knowledge work into controlled AI workflows, without rebuilding the systems of record that already hold your data, and without the data-risk of pointing a model at everything at once.

**Who this is for:** anyone on a team that runs the same work on a cycle (monthly reports, request queues, decision pipelines, post-mortems) and wants AI to speed it up without giving it free run of the organization's data or final say over decisions. In practice that means an operations lead, a team manager, a head of a function, or whoever owns AI and tooling.

**What this is not:** a replacement for your CRM, your accounting or ERP platform, your ticketing or project tracker, your data warehouse, or your HRIS; a database; a compliance-approval system; a prompt library; or a way to skip human review.

## What this is

A setup guide for putting AI to work in ways that are actually useful, compliant, and auditable.

Most teams land at one of two extremes: avoiding AI because they cannot control it, or pointing it at everything and trusting output they cannot verify. This guide is the path between them. It helps your team stand up AI workflows for the recurring work you already do, like producing reports, handling request queues, running decision pipelines, and learning from outcomes. It adds the controls that keep the model on your organization's voice and rules, keep your systems of record (not the model) as the source of truth, and keep it out of decisions it should not make.

It works in three parts: reference files that show where AI genuinely helps and where it does not (constraints), example workspaces you can copy and study (architectures), and skills that interview you and assemble a starting workspace from your answers (skill-starters). Together they take you from "we should use AI" to a working, governed setup.

There are no copy-paste templates here. The value is the structure underneath: knowing which work belongs to AI and which belongs to your platform, database, or established software, and setting it up so the result holds up to a customer, an auditor, or your own team six months later.

## The principle behind all of this

Every repeatable workflow has steps. Every step has a scope of information it actually needs. The job is to match those two things so each step runs with signal instead of noise.

Whatever your environment supports for separating information is your implementation layer. Folders, tabs, knowledge sources, a shared drive, document libraries. The medium changes. The logic does not.

The question is always the same: does this piece of information belong at this step, or am I just carrying it because I do not know where else to put it?

## How the layers stay separate

The toolkit keeps methodology, organization context, and live workflow context in different places:

- `_shared-config/` is organization-level truth: the org profile, voice, setup progress, and reusable learnings.
- `workspaces/` is workflow-level operating context: the live pipeline, queue, cycle, or learning loop.
- `architectures/`, `constraints/`, and `skill-starters/` are toolkit methodology: the reusable shapes, principles, and builders.
- After finalize, methodology moves to `_kit/`; organization context and live workspaces stay visible at the root.

## Most work is not an AI task

Roughly 60% of what people throw at AI is better handled by traditional software, databases, or an established process. Another 30% suits rule-based automation or a prebuilt routine. Only about 10% genuinely needs the judgment a language model brings.

So if you are reaching for Claude to recompute a number your finance platform already owns, you are spending tokens on something deterministic. The constraint files tell you when that is the case.

## Your data

The toolkit is plain files on your machine. It has no server or database of its own and uploads nothing on its own. Setup scopes each step to just the files it needs, so the model is never pointed at everything at once.

Two caveats. Whatever AI tool you use sends the context it reads to that tool's model provider, so apply your organization's policy on what may go to which model, and use an enterprise or zero-retention plan if your data calls for it. And your systems of record stay the source of truth: you connect them, the workflows read from them, and nothing writes back or goes to a stakeholder without a human in the loop.

## How to use this

### Before you start (if you have never used an AI agent)

**What you need:** an AI coding assistant backed by a capable model (a Claude plan, or Cursor, Copilot, Codex, or the Gemini CLI with their own model), and this repo. No server, no database, no Git required. The toolkit is free; you pay only for the AI tool you use. If you do not have an agent yet, set one up once:

1. **Get an AI agent.** Install [Claude Code](https://claude.com/claude-code) or open [claude.ai/code](https://claude.ai/code). (Cowork, Cursor, or VS Code with an AI extension also work.) If your organization already has one, use that.
2. **Download this repo.** Click the green **Code** button, then **Download ZIP**, and unzip it. (Know Git? Clone it instead.)
3. **Open the folder in your agent** and say `Run setup`.

Setup asks a few questions about your organization and builds your first workspace; later, say `add a workflow` to build another. You never open or edit a file yourself.

**Any agentic tool works:** Claude Code, Cursor, Codex, Copilot (agent mode), or the Gemini CLI. Anything that can read this repo and act on it qualifies. A plain browser chat (ChatGPT, Gemini) cannot run setup, but can still use the reference material below.

### Agent startup files

`AGENTS.md` is canonical. Codex, Cursor, Copilot agent mode, Gemini CLI, and other AGENTS-aware tools should read `AGENTS.md` first.

`CLAUDE.md` exists only for Claude Code compatibility. Claude Code loads it, then follows its `@AGENTS.md` import.

Do not copy project instructions into `CLAUDE.md`. If setup or finalize rewrites the operating map, it rewrites `AGENTS.md`.

Everything below is background you can skip.

---

**Just want the reference material?** You do not need setup. The constraint files are portable: open whichever matches your problem, a couple at a time, not all at once. They work anywhere: a Claude Code, Cursor, or VS Code workspace; as knowledge sources in Claude Projects; or pasted into ChatGPT, Copilot, or any chat.

### The last step: finalize

Once you have built the workflows you need, finalize the repo. Say "finalize" (or "make this our operating system") and the agent moves the toolkit itself (`SETUP.md`, `architectures/`, `constraints/`, `skill-starters/`) into a `_kit/` folder, leaving only your organization's workspaces and operating-system map at the root. The repo stops reading like a kit you are setting up and starts reading like the system you run your team on.

You keep building exactly as before: "add a workflow" still works, it just pulls from `_kit/`. And it is fully reversible: finalize writes a `_kit/RESTORE.md` that puts everything back. Treat this as the step that turns the toolkit into your operating system, not an afterthought.

## What is in here

At the root are the toolkit folders, shared organization config, plus three files that run the
toolkit and that you rarely edit directly: `AGENTS.md` (canonical project instructions and
operating map), `CLAUDE.md` (Claude Code wrapper only), and `SETUP.md` (the engine that builds and
adds workflows). Setup creates a `workspaces/` folder for the workflows you build.

```
AGENTS.md        canonical instructions and operating map
CLAUDE.md        thin Claude Code wrapper that imports AGENTS.md
SETUP.md         the engine that builds and adds workflows
_shared-config/  org profile, voice, setup progress, and learnings
constraints/     the principles (10 files)
architectures/   the four shapes + worked examples
skill-starters/  the builders setup runs (5)
workspaces/      the workflows you build (created by setup)
```

### [/constraints](constraints/) (10 files)
The constraints are the principles for getting real work out of AI instead of plausible-looking output. Each of the ten takes one way AI predictably breaks down (writing in a flat, generic voice, losing track of your instructions in a long chat, or trusting a document it should not) and tells you why it happens and how to keep it reliable. Each ends with a few questions that tailor the fix to how your organization works.

These are foundational principles of AI and computer science. They hold for anyone working with a language model.

If you read only two, read [constraint 06 (Layer Triage)](constraints/06-layer-triage.md) and [constraint 09 (Platform Boundary)](constraints/09-platform-boundary.md). The first tells you which problems at your organization are even worth pointing AI at. The second tells you what to build yourself and what to leave to your platform. Those are the two calls most teams get wrong.

### [/architectures](architectures/) (4 shapes + worked examples)
Real folder structures you can copy and adapt. Each is built on one of four shapes. A **gated decision pipeline** moves one item through go/no-go stages to a decision (hiring, a sales pipeline, a project to launch). A **recurring operations queue** runs intake, process, deliver, per request (support escalations, vendor onboarding, access requests). **Recurring document production** turns verified data into a drafted, distributed document on a cycle (a monthly board report, a customer QBR, a status update). A **learning loop** captures an outcome, analyzes it, and reads it back so the work compounds (win/loss reviews, incident retrospectives, underwriting backtests).

Not one of the four? Say "add a workflow" and setup classifies yours by shape and builds from the nearest; if it fits no shape, it builds from scratch using constraints 03, 06, 08, and 09. Each architecture also maps, step by step, what is the AI's job, what a tool or automation handles, and what belongs to your platform of record where the data lives.

Four ship with a fully worked `_examples/` so you see finished output, not the empty shape: a hiring pipeline where a candidate moves from application through screen, evaluation, and decision; a support-escalation queue from intake through triage to a customer-facing response; a monthly board report where every figure traces to its data pack; and a sales win/loss store where closed opportunities are root-caused, written to a pattern store, and read back to sharpen the next pursuit.

### [/skill-starters](skill-starters/) (5 diagnostic skills)
Skills that ask before they build. Each opens with diagnostic questions about your workflow, then assembles a workspace skeleton from your answers: the decomposition logic is built in, your answers supply the specifics. One per shape — gated-decision-pipeline-builder, recurring-operations-queue-builder, recurring-document-production-builder, learning-loop-builder — plus build-from-scratch for work that fits no shape cleanly.

---

Built by Matt Weigand. Released under the [MIT License](LICENSE). Clone, customize, and use it freely.
