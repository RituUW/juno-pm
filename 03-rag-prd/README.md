# 03 — RAG / AI PRD (Module 3)

Juno's "Evidence Engine": the AI PRD specifying what data it's grounded in, how it retrieves and scores evidence, its cost/latency budget, and its failure modes.

## What's here

- [`prd.md`](prd.md) — full AI PRD: Problem, Users + Jobs, Solution (Strategy Mode / Quality Mode / anti-pattern flagging), Data Corpus + Retrieval Strategy (hybrid RAG, top-6, 12mo Jira / 90-day Slack-CRM), Eval Plan, Failure Modes + Guardrails, Success Metrics, and Open Questions.

## Self-review status

- ✅ All three AI-specific sections present: data corpus + retrieval, eval plan, failure modes + guardrails
- ✅ RAG decision (Hybrid: semantic + metadata filtering) justified against cost/speed/accuracy
- ✅ Failure modes cover fabricated citations, overconfident low-evidence ranking, PII leakage; prompt-injection mitigation is flagged as an open question rather than glossed over
- ✅ Eval plan is testable (100% citation coverage, 0% silent-guess rate) and links to `06-evals/eval-stack.md`
- ✅ Retrieval strategy specifies chunking approach, top-k (6), and hybrid similarity/metadata filtering
