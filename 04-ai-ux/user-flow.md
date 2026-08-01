# Juno PM — AI User Flow (the Iceberg)

_Version 1.0 — RocketShip strategic-alignment flow. Produced via M4 AI User Flow Architect._

## Above the waterline

### 1. Trigger
A PM opens Juno before a roadmap review and pastes/uploads raw artifacts (Jira export, Slack thread, support ticket, CRM notes), or clicks "Generate Opportunity Brief" for the current sprint cycle.

### 2. Act
The PM sees the draft Opportunity Brief with inline citations (Artifact/source IDs) on every insight. They can expand any insight to see its scoring rationale, flag conflicting signals side-by-side when sources disagree, and click "Override" on any recommendation with a required free-text reason.

## Below the waterline

### 3. Sense
Juno detects the entry-point payload type — a pasted transcript, an uploaded file, or a "Generate Brief" trigger tied to the current sprint cycle — and identifies which knowledge-base channels (Jira, Slack, support, CRM) are relevant to the artifact(s) provided.

### 4. Retrieve
Hybrid semantic + metadata search pulls the Top 6 evidence segments from Jira (trailing 12 months), Slack/CRM (trailing 90 days), and support tickets — ranked by recency, business impact, and strategic alignment.

### 5. Reason
Each retrieved insight is weighted 0–1 using the Revenue / Risk / Friction rubric. Conflicts between sources (e.g., Sales pushing a feature vs. Engineering flagging system risk) are explicitly flagged rather than silently resolved or averaged.

### 6. Reflect
A citation-linking pass verifies every insight traces to a named source artifact before assembly — no unsourced claims reach the draft. The brief is then assembled into the Opportunity Brief structure (Problem, Persona, Evidence Table, Risks, Next Experiment) within the 50K-token budget; if evidence is too sparse to support a confident ranking, that item is marked "insufficient evidence to prioritize" instead of being scored.

### 7. Recover
If retrieval or scoring fails outright, Juno surfaces the failure rather than a silent empty state. If a PM overrides a recommendation, that override — and its stated reason — is logged and fed back into the knowledge base so next quarter's brief can check whether Juno's original signal was right in hindsight. This is the loop that trains trust over time.

## UX touchpoints

| Node | What user sees | What user can do |
|---|---|---|
| Trigger | Upload/paste area + "Generate Opportunity Brief" button | Paste or upload raw artifacts; kick off a run for the current sprint cycle |
| Retrieve → Reason | "Juno is thinking…" status with a pulsing loading state while retrieval and scoring run | Wait, or cancel and re-trigger with different/added artifacts |
| Reflect | Confidence/evidence label per insight ("insufficient evidence to prioritize" when applicable) | Expand an insight to see its full scoring rationale and cited source(s) |
| Act | Draft Opportunity Brief with inline citations and side-by-side conflict flags | Expand rationale, view conflicting signals, click "Override" with a required reason |
| Recover | Error/fallback state on retrieval or scoring failure; logged override history | Retry the run; review past overrides against this quarter's outcome |
