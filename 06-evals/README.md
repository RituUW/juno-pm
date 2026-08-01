# 06 — Evals (Module 6)

The trust architecture that keeps Juno's judgment matching a Senior PM's: a three-layer eval stack (online, human, automated) plus the human grading rubric behind it.

## What's here

- [`eval-stack.md`](eval-stack.md) — Layer 1 (Accept/Reject/Edit + passive edit-rate tracking, per request), Layer 2 (weekly Senior-PM-graded sample against the human rubric), Layer 3 (automated missing-citation gate + unverified-capability guardrail, 0% tolerance, every draft).
- [`human-rubric.md`](human-rubric.md) — 4 anchored dimensions (Strategic Alignment, Citation Correctness, Technical/Risk Depth, Safety), sampling cadence, graders + tiebreaker, and disagreement protocol.

## Self-review status

- ✅ Eval stack covers all 3 layers (user feedback, human eval, automated)
- ✅ Each layer has a numeric pass bar (40% edit-rate ceiling; 4/5 mean + 5/5 zero-tolerance dims; 0% citation-gate tolerance)
- ✅ Human rubric has 4 anchored dimensions
- ✅ Safety is an explicit dimension (unverified-capability guardrail)
- ✅ Disagreement protocol is explicit (>1-point gap → third-grader tiebreak)
- ✅ Golden set is versioned — seeded from the 5 RocketShip artifacts, expanded from real weekly cycles

## Still open

- The top-level repo `README.md` PM Execution Plan (Where / Next / Watch / Red Lines / Governance) is the last certification step, finalized via the Final Project Deliverables Builder tool once all 6 modules are committed.
