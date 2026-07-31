# Juno PM — AI Solution Decision Matrix


| Lens | Score (1–5) | Notes |
|---|---|---|
| Value | 5 | Directly fixes the "loudest voice wins" prioritization failure — lets PMs defend a "no" or "not now" with evidence instead of opinion. |
| Feasibility | 4 | RAG over existing artifacts (transcripts, tickets, CRM notes, Slack) is achievable now with no new data integrations; the harder lift is the review/approval workflow around it, not the retrieval itself. |
| Cost | 3 | Requires building and maintaining a RAG pipeline plus a human-review step before any ranking reaches leadership — real setup and ongoing curation cost, though lower than a fine-tuned model. |
| Risk | 3 | Core failure mode (silently burying a compliance/security signal because it wasn't phrased urgently) is real and high-consequence; mitigated by a hard-coded review rule, but that guardrail must be maintained and trusted, not "set and forget." |
| Speed-to-impact | 4 | Copilot draft-and-review is a lighter lift than full autonomous ranking, so the 75% prep-time reduction (2 hrs → 30 min) is reachable within a quarter, not a multi-quarter build. |
| Defensibility | 5 | Every insight in the Opportunity Brief is grounded and cited to a specific source artifact, with severity scored by evidence and consequence — not by authority, tone, or deadline proximity. |

**Total: 24/30**

## Strongest lens
**Defensibility.** Because Juno is grounded in RAG against the actual uploaded artifacts rather than reasoning from general knowledge, every claim in the brief traces back to a named source (e.g., "Artifact 4: Sales Rep Call Notes"). That traceability is exactly what turns Juno's output into something a PM can defend to a stakeholder or reviewer, rather than another opinion in the mix.

## Weakest lens
**Cost.** The bet requires standing up and maintaining a RAG pipeline across multiple messy, non-uniform input types (transcripts, tickets, emails, CRM notes, Slack threads) plus a human-in-the-loop review workflow — real engineering and process investment with no cost estimate yet. This would improve once the RAG infrastructure is built once and reused across weekly cycles, dropping the marginal cost per brief, and once the review step is scoped tightly enough (e.g., only flagged/high-severity items get full PM review) rather than requiring a full re-check of every generated brief.
