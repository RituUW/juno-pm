# Juno PM — Agent Control Panel

_Version 1.0 — Produced via M5 Agent Control Panel tool, built on the AWSpec (`awspec.md`)._

> The PM-facing dashboard for an agent: what to watch, what to throttle, what to roll back. Defines the on-call surface for Juno in production.

## Observability — what we trace

| Field | Notes |
|---|---|
| Trace ID | One per brief-generation run, ties Plan → Execute steps together for audit |
| Trigger payload | The raw artifact(s) submitted + whether a strategy document was attached (Strategy Mode vs. Quality Mode) |
| Retrieved chunks | The Top 6 evidence segments pulled per query, with source (Jira/Slack/CRM/Support) and freshness window |
| Tool calls | Which read-only APIs were called (Jira, Slack, CRM, Support Ticket System) and the internal Evidence/Override Log write |
| Outputs | Final Opportunity Brief content, insight-level priority (P0–P3), `strategicPillar`, `strategicAlignment` |
| Confidence per risk | `strategicAlignment` score (0–100) per insight; flags "Low Confidence" (<40) and `notRecommended` items |
| Latency (p95) | Time from trigger to completed brief; SLA ceiling is 60s per the AWSpec timeout stop condition |
| Tokens + cost | Tokens consumed per run against the ~50K-token cost ceiling per brief |

## Throttles

| Lever | Default | When to change |
|---|---|---|
| Concurrency | 1 run per PM at a time | Raise only if multiple PMs need simultaneous brief generation during a shared roadmap cycle |
| Max tokens / run | ~50,000 tokens | Raise only with a documented cost-ceiling exception; prefer summarizing/chunking sources first |
| Tool-call budget / run | 4 read calls (Jira, Slack, CRM, Support) + 1 write (Override Log) per the fixed Planner-Executor pipeline | Increase only if a new source type is added to the corpus in a future PRD revision |
| Per-day spend cap | Set at a level that supports one full team's weekly roadmap cycle plus reruns; lower it if a single team is consuming a disproportionate share | Lower immediately if a runaway loop or repeated retries is detected |

## Kill switches

- `juno-brief-generation` feature flag → off if the fail-safe "insufficient evidence to prioritize" state stops firing (i.e., Juno starts producing confident-looking briefs from sparse evidence) — this is the core trust guarantee and cannot silently degrade.
- Rollback path: disable the flag, fall back to the pre-Juno manual prioritization process, and replay the affected run's trace log to diagnose before re-enabling.

## On-call playbook

1. **Symptom:** A PM reports a brief with an uncited claim, a hallucinated metric, or a citation that doesn't support the insight.
2. **First check:** Pull the run's trace — confirm whether the citation-linking pass actually ran, and whether the cited source segment matches the claim.
3. **Remediation:** If the citation-linking pass was skipped or failed silently, kill the `juno-brief-generation` flag and roll back; if it's an isolated retrieval-ranking miss, log it and lower the confidence threshold for that source type until the ranking logic is corrected.
4. **Escalation path:** Escalate to the PM's manager only if a wrong, uncited recommendation reached leadership before being caught — otherwise resolve within the triad (PM + Raj) and log the incident for the next `06-evals` human-review batch.
