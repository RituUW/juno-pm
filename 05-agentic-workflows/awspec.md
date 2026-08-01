# Juno PM — Agent Workflow Spec (AWSpec)

_Version 1.0 — Produced via M5 Agent Workflow Spec Builder._

## 1. Goal
Juno autonomously retrieves, scores, and drafts a fully-cited Opportunity Brief each cycle so a PM gets a defensible, evidence-backed draft instead of manually assembling one — without ever publishing a decision or resolving a stakeholder conflict on its own.

## 2. Trigger
A PM pastes/uploads raw artifacts (Jira export, Slack thread, support ticket, CRM notes) or clicks "Generate Opportunity Brief" for the current sprint cycle, ahead of a roadmap review.

## 3. Inputs
Required context for the run: the raw artifact(s) provided (transcript, ticket, email, call notes, Slack thread), an optional RocketShip strategy document, and the current knowledge-base windows (Jira 12mo, Slack/CRM/support 90 days).

## 4. Tools available
| Tool | Scope | ACL |
|---|---|---|
| Jira API | Read-only | Last 12 months of epics/stories/defects |
| Slack API | Read-only | `#support` and `#backend-monitoring` only, last 90 days, no DMs |
| CRM/Sales Notes API | Read-only | Last 90 days, excludes closed deals older than 12 months |
| Support Ticket System | Read-only | Excludes tickets tagged "spam" or "test" |
| Internal Evidence/Override Log | Write | Logs PM overrides and brief outcomes for next quarter's Linked memory |

Juno has **no write access** to Jira, Slack, CRM, or any customer-facing system — it can only read evidence and write to its own internal log. It cannot create tickets, send Slack messages, or modify CRM records. All tool calls must be attributable through an audit log.

## 5. Memory
- **Contextual (short-term) — IN:** the current artifact batch for this run only; pulled fresh each cycle, not retained across runs.
- **Linked (long-term/episodic) — IN:** logged PM overrides and prior briefs, referenced to check whether Juno's past recommendations proved correct in hindsight.
- **Episodic (per-conversation turn memory) — OUT:** Juno does not carry conversational state between unrelated runs.
- **Semantic (general world-knowledge memory) — OUT:** Juno reasons only from retrieved evidence and the strategy document, not from an evolving internal semantic memory, to avoid drifting from source-grounded scoring.

## 6. Pattern
**Planner-Executor.** ReAct isn't the right fit — Juno's steps are a fixed pipeline per brief, not an open-ended loop of reasoning and re-planning based on unpredictable tool feedback; there's no ambiguous "which tool next" decision to react to at each step.

- **Step 1 (Plan):** Given the query + artifacts, Juno plans which sources to retrieve from (Jira, Slack, CRM, tickets) and in what order, based on artifact type.
- **Step 2 (Execute):** Retrieves the highest-ranked evidence segments from the knowledge base.
- **Step 3 (Execute):** Runs the scoring/weighting function (0–1) and checks for source conflicts.
- **Step 4 (Execute):** Drafts the Opportunity Brief within the 50K-token budget, attaching citations.

## 7. Stop conditions
- **Success:** brief is assembled within the token budget with every insight citing a source artifact.
- **Failure:** retrieved evidence is too sparse or conflicting to support a confident ranking — Juno returns "Insufficient evidence to prioritize" for that item rather than guessing.
- **Escalation:** two or more sources contradict each other (e.g., Sales vs. Engineering) — Juno surfaces both and flags the conflict for the human to resolve; it never silently picks a side.
- **Timeout:** if a run exceeds the 60-second latency SLA for a full brief, Juno aborts and returns a partial-result flag rather than an incomplete brief presented as complete.

## 8. Handoff rules
Any insight with a `strategicAlignment` score below 40 is auto-labeled **"Low Confidence"** in the Evidence Table rather than presented as a firm recommendation, and requires explicit PM confirmation before it's treated as ranked. Any insight flagged `notRecommended` (multiple anti-patterns present) is routed directly to human review before it can enter the final brief. In both cases, the PM's decision (confirm / override with reason) is written back to the Internal Evidence/Override Log.

## 9. Eval hooks
For each run, Juno logs: the retrieved evidence set per insight, the computed weight/score and its rationale, any conflict flagged and how it was surfaced, whether the "insufficient evidence" fail-safe fired, latency and token spend, and — post-brief — any PM override with its stated reason. This log is what feeds the [`06-evals/eval-stack.md`](../06-evals/eval-stack.md) automated and human-review layers, and lets next quarter's brief check whether a past recommendation was right in hindsight.
