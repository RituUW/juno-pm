# Juno PM — AI-UX Trust Gap Mitigations

_Version 1.0 — Produced via M4 AI-UX Trust Gap Checker._

## Gap 1 — Black-box gap
*Users don't know why the AI did what it did.*

- **Where it shows up in Juno:** the Reflect/Act nodes — a PM sees a ranked Opportunity Brief but, without more, can't tell why one insight outranked another.
- **Mitigation:** every insight carries an inline citation (Artifact/source ID) and is expandable to show its full scoring rationale — the PM can trace any ranking back to the specific evidence and weight that produced it, rather than trusting a bare score.

## Gap 2 — Hallucination gap
*Users don't know when the AI is wrong.*

- **Where it shows up in Juno:** the Reason/Reflect nodes — a confidently-formatted brief can look equally authoritative whether the evidence behind it is strong or thin.
- **Mitigation:** a citation-linking pass runs before any insight reaches the draft, and when evidence is too sparse or conflicting to support a confident ranking, that item is explicitly labeled "insufficient evidence to prioritize" and flagged for human review — Juno never produces a best-guess score that looks as certain as a well-evidenced one.

## Gap 3 — Control gap
*Users don't know what they can or cannot change.*

- **Where it shows up in Juno:** the Act node — a PM disagreeing with a ranking needs a real, first-class way to change it, not just to ignore the brief.
- **Mitigation:** every recommendation has an "Override" action requiring a free-text reason; the override and its rationale are logged and resurfaced in the next quarter's brief so the PM (and Juno) can check whether the override was right in hindsight.

## Cross-gap fail-state

If all three gaps fire at once — Juno cites a source that doesn't actually support the claim (black-box gap masking a hallucination), while presenting it with a confident-looking score (hallucination gap) that the PM has no easy way to challenge (control gap) — the failure mode is a wrong, confidently-styled priority silently entering the roadmap. The UI it goes into: the same "insufficient evidence" fail-safe state used for sparse evidence is Juno's last line of defense — the citation-linking pass (Reflect) is designed to catch a broken citation *before* the brief renders, converting what would be a silent bad ranking into a visible "insufficient evidence to prioritize" flag with a required Override path instead.
