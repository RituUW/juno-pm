# Juno PM — Eval Stack

_Version 1.0 — Produced via M6 Eval Stack Designer._

**Definition of "good":** Juno's output must meet all 3 to be considered Associate-PM quality — **strategically aligned** (every prioritization decision traces back to RocketShip's Guiding Principle — trust/reliability/governance over feature volume — not to whoever asked loudest), **fully grounded** (every claim, metric, and risk cites a specific source artifact; zero invented specifics), and **conflict-aware** (surfaces contradictions between stakeholders, e.g., Sales vs. Engineering, explicitly, rather than silently resolving or averaging them).

## Layer 1 · User feedback (Online Evals — every use)

- **Signals captured:**
  - *Active:* an Accept / Reject / Edit mode on every insight in the Evidence Table and every claim in the drafted PRD. Accept = no changes needed; Reject = insight is wrong or irrelevant, requires a one-line reason; Edit = correct it inline. This captures which specific claim failed, not just overall satisfaction.
  - *Passive:* % of generated text edited before export (diffing the draft PRD against the final exported version), paired with regeneration count (how many times a PM re-ran the brief before accepting the first draft).
- **Cadence:** per request.
- **Pass bar:** less than 40% of generated text edited before export. Consistently crossing 40%+ is a strong signal Juno is creating an intelligence tax rather than scaling judgment, even with no explicit complaints.
- **Who acts on it:** the requesting PM in the moment (Accept/Reject/Edit); the PM triad reviews the passive edit-rate trend weekly.

## Layer 2 · Human evaluation (System-Level Evals — sampled drafts)

- **What gets sampled:** every brief containing a P0/P1 insight, plus a random 10% sample of P2/P3-only briefs, to build a golden dataset that reflects real strategic judgment, not just easy cases.
- **Rubric:** see [`06-evals/human-rubric.md`](human-rubric.md) — Strategic Alignment, Citation Correctness (Hallucination Check), Technical/Risk Depth, and Safety.
- **Cadence:** weekly batch.
- **Pass bar:** mean score ≥4/5 on Strategic Alignment and Technical/Risk Depth; Citation Correctness and Safety must both score 5/5 (zero-tolerance dimensions — a single uncited or unverified-but-stated-as-fact claim fails the brief regardless of the other scores).
- **Who grades:** a Senior PM, with a second Senior PM (or the PM's manager) as tiebreaker on any disagreement.

## Layer 3 · Automated evals (Component-Level Evals — every draft)

- **Golden set:** seeded from the 5 RocketShip artifacts (user interview, support ticket, executive email, sales call notes, Slack thread) with their known-correct Revenue Blocker / System Risk / User Friction labels; expanded as real weekly cycles produce human-graded outcomes.
- **Eval checks:**
  - **Missing-citation gate (LLM-as-a-Judge):** scans the drafted PRD and flags any sentence in the Evidence Table, Risks, or Problem Summary that makes a specific factual claim (a number, date, quote, or named system) without an attached Artifact/Source ID citation.
  - **Unverified-capability guardrail:** Juno is not permitted to state a technical risk, blocker, or capacity assumption (e.g., "Engineering can ship SSO by October 1st") unless a specific artifact confirms that capability or timeline; if no artifact confirms it, it must be labeled an unverified assumption in the Risk section, not stated as fact.
- **Cadence:** every draft, before it reaches a human PM.
- **Pass bar:** **0% tolerance** — a single uncited factual claim, or a single unverified capability claim stated as fact, automatically blocks publication. Citation and capability-verification are binary trust requirements, not soft quality metrics, so the gate triggers on the first occurrence rather than a percentage threshold.
- **Who acts on it:** the automated gate blocks the draft from reaching the PM; the PM triad owns the bar and reviews any gate-triggered block during the weekly human-eval batch.
