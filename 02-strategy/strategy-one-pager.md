
# Juno PM — AI Strategy One-Pager

Version 0.1 — placeholder. Replace via M2 AI Strategy One-Pager Builder.

## Bet

We are betting that grounding Juno in our actual artifacts (transcripts, tickets, CRM notes, Slack threads) and having it draft a scored, evidence-cited prioritization ranking — reviewed by a PM before it reaches leadership — will replace "loudest voice wins" roadmap decisions with a defensible, evidence-based process.

## Why now

RocketShip's signal collapse (P0 threads, thousands of tickets, lost deals) has outgrown manual triage, and RAG-grounded LLMs are now reliable enough to synthesize messy, mixed-format inputs (text, tickets, call notes) into structured, source-cited output — a capability that wasn't affordable or trustworthy enough to run on real prioritization decisions 18 months ago.

## AI value proposition (pick one and commit)

**Mitigate risk.**

Juno's core job is preventing the costly failure mode already happening at RocketShip: reacting to the loudest stakeholder (an angry enterprise email, a CEO's feature whim) instead of the highest-consequence one, which risks burying a compliance-blocking deal or a fragile system collapse under louder but lower-stakes noise. (The 75% prep-time reduction is a real secondary benefit, but the bet is justified on decision quality, not time saved.)

## Three-layer placement

* **Foundation layer:** General-purpose base LLM (reasoning over messy, unstructured notes to find themes and reformat qualitative input into a scoring template).
* **Application layer:** RAG grounded against the actual uploaded artifacts (transcripts, tickets, CRM notes, Slack threads) so every claim traces to a source, plus a Copilot pattern that drafts a first-pass ranked backlog with written reasoning for PM review.
* **Experience layer:** Shows up as a one-page Opportunity Brief with an evidence table and severity scores, delivered to the PM before any priority is synced to Jira or presented to leadership.

## Jobs × Risk × Autonomy

* **Jobs:** Synthesizing raw, unstructured artifacts into a structured, evidence-linked Opportunity Brief, and producing a first-draft ranked backlog with reasoning attached to each item.
* **Risk:** Juno silently drops or downweights a real compliance/legal/system risk (e.g., a security-certification deadline) because it wasn't phrased urgently, causing leadership to miss a deal-breaking issue until it's too late to fix.
* **Autonomy:** Decide-with-review (**Copilot**) — Juno drafts the scored ranking and reasoning; a human PM makes the final prioritization call before anything reaches leadership or gets synced to Jira. **Not Agent** — full autonomous ranking/routing risks burying a low-scored-but-politically-critical signal with no accountable person to catch it.

## Success metric

Weekly roadmap-prioritization meeting prep time reduced by 75% (2 hours → 30 minutes) by end of Q4 2026, with every prioritized item traceable to a cited source artifact.

## Red lines

Pull this bet immediately if: Juno fails to flag an artifact mentioning compliance, security certification, or a contractual deadline for mandatory human review (regardless of its computed score); if Juno's evidence citations turn out to be fabricated or untraceable to a real source artifact; or if PMs start rubber-stamping Juno's draft ranking without reviewing the underlying evidence, defeating the purpose of the Copilot (not Agent) design.
