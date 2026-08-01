# 04 — AI-UX (Module 4)

How Juno's judgment surfaces to the user: the full Iceberg flow (above/below the waterline) and the three trust gaps it has to close to be usable.

## What's here

- [`user-flow.md`](user-flow.md) — the AI Iceberg: Trigger and Act above the waterline; Sense, Retrieve, Reason, Reflect, and Recover below it, plus a UX touchpoints table mapping each node to what the user sees and can do.
- [`trust-gaps.md`](trust-gaps.md) — the three trust gaps (black-box, hallucination, control) with where each shows up in Juno's flow, its specific mitigation, and a cross-gap fail-state describing what happens if all three fire at once.

## Self-review status

- ✅ All 7 nodes of the AI Iceberg specced with a UX treatment, not just backend behavior
- ✅ All three trust gaps addressed with a concrete UI pattern each (citation chips, "insufficient evidence" labeling, logged Override)
- ✅ The Act node names what's reversible (Override with logged reason) vs. what Juno can't do (publish, resolve conflicts)
- ✅ The Recover node has a real path — visible error/fallback state plus override history feeding the next cycle, not just an apology
