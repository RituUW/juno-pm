# Juno PM

**An AI Associate PM copilot that turns raw, messy signal — interviews, tickets, emails, call notes, Slack threads — into evidence-backed, strategy-aligned product decisions.**

[**Live prototype →**](https://clarify-transcript-flow.lovable.app/)

![Juno dashboard with strategy loaded and insights scored against detected pillars](01-prompting/juno-strategy-mode-dashboard.png)

## The problem

Product teams drown in signal: support tickets, sales call notes, executive requests, engineering warnings, user interviews — all arriving at once, in different formats, with different urgency and different actual consequence. Without a systematic way to weigh them, prioritization defaults to whoever is loudest — an angry enterprise ticket, a CEO's feature whim — rather than whoever has the strongest evidence and the highest real business risk. That's not a prioritization process; it's noise management.

Juno is built to fix that: it ingests raw artifacts, scores and ranks them against a real strategic document (or against request quality when no strategy doc is available), cites its evidence for every claim, flags conflicting signals instead of silently resolving them, and automatically escalates high-risk, low-alignment items instead of letting them sink quietly to the bottom of a list.

## What Juno does

- **Reads raw input live** — transcripts, tickets, and notes are processed as they're typed or pasted, no manual "run" step.
- **Grounds every score in evidence** — insights are ranked with a confidence score and a citation back to the specific source artifact and (when available) the specific strategic pillar they support.
- **Auto-detects strategy** — uploading a strategy document extracts its actual pillars and re-scores every insight against them, instead of relying on a hardcoded framework.
- **Flags risk automatically** — low-alignment or high-risk insights are pulled into a dedicated risk assessment panel with a mitigation plan, an assigned stakeholder, and a one-click Slack handoff, rather than being buried in a ranked list.
- **Drafts an editable, section-by-section PRD** — each section can be manually edited or independently regenerated, so fixing one section never discards work done on another.
- **Hands off directly to real tools** — a Command Center bar sends a brief straight to Slack or spins up a Jira ticket, instead of requiring a manual copy-paste.

## Repository structure

| Folder | What's in it |
|---|---|
| [`01-prompting/`](01-prompting/) | Juno's core system prompt (persona, task boundaries, scoring constraints, chain-of-thought rules) and the live prototype write-up + screenshots |
| [`02-strategy/`](02-strategy/) | The strategic bet behind Juno — why it's worth building, scored across six decision lenses, with a numeric success metric and named red lines |
| [`03-rag-prd/`](03-rag-prd/) | The full AI PRD: problem, users, solution, retrieval architecture (RAG data corpus, chunking, top-k, conflict resolution), eval plan, and failure modes + guardrails |
| [`04-ai-ux/`](04-ai-ux/) | The end-to-end user flow (trigger through recovery) and how Juno closes the three core AI trust gaps — black-box, hallucination, and control |
| [`05-agentic-workflows/`](05-agentic-workflows/) | The agent workflow spec (goal, tools, memory, pattern, stop conditions, handoff rules) and the on-call control panel for running Juno in production |
| [`06-evals/`](06-evals/) | The three-layer eval stack (user feedback, human evaluation, automated checks) and the human grading rubric that defines "good" |

## Architecture at a glance

- **Foundation:** a general-purpose LLM reasoning over messy, unstructured input.
- **Grounding:** hybrid RAG (semantic + metadata search) over Jira, support tickets, CRM/sales notes, and Slack — read-only, with defined freshness windows and explicit exclusion rules (no stale data, no personal DMs, no HR/compensation data).
- **Orchestration:** a fixed Plan → Retrieve → Score → Draft pipeline (not an open-ended agent loop), with a citation-linking pass before anything reaches a human, and hard stop conditions for insufficient evidence, unresolved conflicts, and timeouts.
- **Human-in-the-loop by design:** Juno drafts and scores; a person reviews, edits, or overrides before anything reaches leadership or gets synced to another system. Every override is logged and checked against the next cycle's outcome.

## PM execution plan

**Where we are:** the system prompt, strategic bet, AI PRD, UX flow, agent spec, and eval stack are all specified and the live prototype demonstrates the full loop — live-sync input, strategy-grounded scoring, automatic risk flagging, editable PRD output, and one-click handoff to Slack/Jira.

**What's next:** connect Juno to real (not pasted-in) Jira, Slack, and CRM data sources; wire the automated citation and unverified-capability gates into an actual CI check ahead of any human review; validate the human-eval rubric with a second grader for calibration.

**What we're watching:** the % of generated text a PM edits before export (a rising edit rate signals Juno is creating work instead of removing it); how often the "insufficient evidence" fail-safe fires versus a confident wrong answer slipping through; override frequency and whether overridden decisions turn out to be right in hindsight.

**Red lines — what would pull this bet:** Juno fails to flag a compliance, security, or contractual-deadline artifact for mandatory human review regardless of its computed score; an evidence citation turns out to be fabricated or untraceable to a real source; PMs start rubber-stamping Juno's draft without reviewing the underlying evidence, defeating the point of keeping a human in the loop.

**Governance:** Juno has no write access to any external system except its own internal evidence/override log — it cannot create tickets, send messages, or modify records on its own. Every recommendation is reviewable, every override is logged, and nothing reaches leadership without a human sign-off.
