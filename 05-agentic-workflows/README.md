# 05 — Agentic Workflows (Module 5)

Juno as a buildable multi-step agent: the Agent Workflow Spec (goal, triggers, tools, memory, pattern, stop conditions) and the PM-facing control panel for running it in production.

## What's here

- [`awspec.md`](awspec.md) — the full 9-section AWSpec: Planner-Executor pattern (Plan → Retrieve → Score → Draft), read-only tool ACLs (Jira/Slack/CRM/Support) plus one write scope (the internal Override Log), Contextual + Linked memory (Episodic/Semantic explicitly out), stop conditions (success/failure/escalation/timeout), and the handoff/confidence-threshold rules.
- [`control-panel.md`](control-panel.md) — the on-call surface: what gets traced per run, throttle levers and defaults, kill switches, and the on-call playbook for a bad (uncited or hallucinated) brief.
- `Juno Agent.json` — optional Langflow starter export for the post-class multi-agent lab (Orchestrator / Strategy Owner / PRD Writer agents).

## Self-review status

- ✅ AWSpec has all 9 sections filled
- ✅ Tools list explicit read/write scope for each tool
- ✅ Memory section names all 4 memory types, each marked in or out
- ✅ ≥3 stop conditions including escalation
- ✅ Handoff rule names a numeric confidence threshold (strategicAlignment < 40)
- ✅ Eval hooks defined — feeds directly into `06-evals/eval-stack.md`
