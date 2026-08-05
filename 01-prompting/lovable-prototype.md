# Juno PM — Prototype

## Live prototype
[https://clarify-transcript-flow.lovable.app/](https://clarify-transcript-flow.lovable.app/)

## GitHub source code
Not yet connected to a separate source repo.

## What this prototype does

Juno is a live, four-panel workspace that turns raw customer/user signal into a cited, editable, action-ready PRD in real time — no manual "run" step required.

**Workspace layout:**
1. **Strategy Document** — optional upload (`.txt`/`.md`) or paste-in field with a live word count. A persistent banner ("No strategy document loaded — insights will not be scored against any strategy") always makes it clear whether Juno is scoring against a real strategy or falling back to general request-quality signals, instead of silently guessing.
2. **Raw Transcripts** — a live input field ("Juno listens as you type") with a running character count and a Clear action.
3. **Structured Insights** — a ranked, live-updating list of insight cards, each tagged with a priority (P0–P3), a strategic category (e.g., Reliability, Growth, User Experience), a sentiment (Positive/Neutral/Negative), and a type (Pain/Request/Delight).
4. **Draft PRD** — a live-generated PRD with copy and download actions and a warning banner whenever it was generated without a strategy document to ground it.

**Live-sync processing (no "Process" button):**
- Input is watched continuously rather than requiring a manual trigger — Juno reacts automatically as a transcript is typed or pasted in.
- A single status indicator in the header reflects Juno's actual processing phase in plain language (e.g., "Thinking," "Synthesizing," "Synced") instead of a generic loading spinner.
- The Draft PRD streams its output as it's generated rather than appearing all at once.

**Evidence and confidence on every insight:**
- Each insight card carries a confidence meter and score (e.g., "High · 92," "Solid · 75") alongside a source citation badge naming the category it was scored against.
- A short rationale explains the score in plain language, and explicitly states when the score reflects general request quality rather than strategic alignment — so the source of the confidence is never hidden.
- Each insight also has a source-tracing icon intended to connect it back to the specific language in the transcript that produced it.

**Editable, section-by-section PRD:**
- Each section of the generated PRD (e.g., "Overview") is independently editable and independently regeneratable — hovering a section reveals an Edit control and a Regenerate control.
- Editing a section turns it into a direct text field for manual refinement. Regenerating re-runs Juno on just that one section, so a section can be fixed or re-drafted without discarding manual edits already made elsewhere in the document.
- The header status indicator confirms when edits have synced and saved.

**One-click handoff:**
- A Command Center bar on the PRD panel includes "Share to Slack" and "Create Jira Ticket" actions, alongside copy and download — so a finished brief can move directly into the tools a PM already uses, rather than requiring a manual copy-paste handoff.

## Strategy-grounded scoring, tested end-to-end
Loading a real strategy document switches the whole workspace into a grounded mode:
- The top banner changes from a "no strategy loaded" warning to an "Active Strategy" state showing the word count and a **Detected Pillars** row — Juno auto-extracts the named strategic pillars directly from the uploaded document rather than relying on a hardcoded list.
- Every insight is then scored against one of those specific pillars, not a generic quality heuristic — e.g., an export-reliability complaint is explicitly tied to a "Reliability" pillar, and a team-sharing request is tied to a "Growth via Retention" pillar, each with its own confidence score and a plain-language rationale explaining the tie.
- This confirms the scoring logic isn't cosmetic — it reads the uploaded strategy, extracts real structure from it, and changes its output accordingly.

**Automatic risk assessment:**
- A dedicated "Risk Assessment" panel surfaces on its own whenever an insight scores low strategic alignment (e.g., 20/100 or 15/100) — instead of letting a low-alignment item sit quietly at the bottom of a ranked list, it's pulled into a separate, high-visibility sidecar labeled by assumption count (e.g., "2 high-risk assumptions").
- Each flagged risk includes the specific low-alignment insight, its alignment score and the reason it's risky, a concrete mitigation plan (e.g., "Conduct 3 user interviews to validate the underlying problem"), an assigned stakeholder (e.g., `@research-team`), and a one-click "Mitigation Slack Message" action to route it to that stakeholder immediately.
- This turns strategic misalignment into something actionable and owned, rather than a number that quietly sinks to the bottom of a list.

## Screenshots

**Strategy-grounded dashboard** — strategy document loaded, pillars detected, a P0 insight scored 95/100 against the "Trust at Scale" pillar with a full rationale:
![Juno dashboard with strategy loaded and insights scored against detected pillars](juno-strategy-mode-dashboard.png)

**Automatic risk assessment sidecar** — two low-alignment insights (a cosmetic nav-bar color request and a dark-mode request) automatically flagged with mitigation plans and a one-click Slack handoff:
![Juno risk assessment sidecar flagging two high-risk, low-alignment insights](juno-risk-assessment-sidecar.png)

**Detected pillars, extracted live from the uploaded strategy document:**
![Juno strategy document panel showing auto-detected strategic pillars](juno-risk-assessment-detected-pillars.png)

**Low-alignment insight detail and editable PRD section** — a UI-polish request scored 20/100 with its rationale, next to the PRD's per-section Edit/Regenerate controls:
![Juno low-alignment insight card next to an editable PRD Overview section](juno-low-alignment-insight-prd-edit.png)

## Design direction
Not yet recorded.

## What this proves out, and what's next
This prototype proves that raw, messy user input can be turned into a live, transparent, strategy-grounded, evidence-linked, editable, and risk-aware prioritization workflow end-to-end — not just a one-shot AI summary, but a working surface a PM could actually use and trust day to day, whether or not a strategy document is available, and with low-alignment items automatically escalated rather than silently buried.
