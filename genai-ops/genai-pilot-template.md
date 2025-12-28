# GenAI Pilot Proposal Template

## Purpose
Run a time-boxed GenAI pilot with clear guardrails and measurable outcomes. Optimize for **toil reduction, decision speed, and quality**—not novelty.

---

## 1) Problem statement (current state + impact)
- What operational burden are we reducing (toil / bottleneck)?
- Who is impacted (roles/teams) and how often?
- What is the cost today (time, cycle time, rework, escalations)?

**Baseline (current state)**
- Current process steps:
- Current cycle time / effort (best estimate):
- Known failure points:

---

## 2) Hypothesis (measurable + time-boxed)
If we deploy **[GenAI solution]** for **[workflow]**, then **[metric]** will improve by **[X]** within **[time]**, without increasing **[risk metric]**.

Example format:
- “Reduce weekly status-update prep time by 30% within 4 weeks without increasing incorrect status reporting.”

---

## 3) Scope (what is / is not included)
**In scope**
- Workflows:
- Data sources:
- Output formats (Jira comment, doc snippet, Slack summary, etc.):

**Out of scope**
- Explicitly list what you will not automate (e.g., final decisions, approvals, external comms).

---

## 4) Users and workflow integration (human-in-the-loop)
- Primary users:
- Where it lives (Jira / Docs / Slack / internal tool):
- Human approval step (what must be reviewed before publishing):
- Training/enablement needed (yes/no):

---

## 5) Guardrails (privacy, security, accuracy)
**Data**
- Allowed data classification:
- Prohibited inputs (PII, secrets, contracts, customer data, etc.):
- Redaction requirements:

**Controls**
- Audit logging (what is logged, retention):
- Access controls (who can use it):
- Prompt/version control (how changes are managed):

**Accuracy + safety**
- Required citations/links back to source artifacts:
- Confidence thresholding (when to abstain):
- Failure modes + mitigations:

**Kill switch**
- Conditions to pause/disable the pilot:
- Owner authorized to disable:

---

## 6) Success metrics (and how we measure)
Define 3–5 metrics max, including at least one quality and one adoption metric.

| Metric | Baseline | Target | Measurement method | Owner |
|---|---:|---:|---|---|
| Time saved / week |  |  | Time study or self-report + sampling |  |
| Adoption rate |  |  | # active users / eligible users |  |
| Quality (error rate) |  |  | Sampling review; % outputs needing correction |  |
| Cycle time impact (optional) |  |  | Jira time-in-status or lead time proxy |  |
| Reduced status churn (optional) |  |  | staleness %, fewer clarifying pings |  |

---

## 7) Rollout plan (time-boxed)
- Pilot group (size + roles):
- Duration (recommended 2–4 weeks):
- Enablement/training:
- Feedback loop (weekly review owner + format):
- Scale criteria (what must be true to expand):
- Exit criteria (what causes us to stop):

---

## 8) Ownership & decision
- Pilot owner (DRI):
- Approvers (Security/Privacy/Eng lead as needed):
- Decision date (go/no-go):

---

## Example (filled): GenAI-assisted Onboarding Q&A Agent (Docs Hub RAG, citation-first)

*Illustrative example — systems, numbers, and names are placeholders.*

## 1) Problem statement (current state + impact)
New joiners ask the same onboarding questions repeatedly across Slack and 1:1s (systems overview, “where is the runbook,” “how do we ship,” “who owns X”). Answers vary by person and may be outdated, creating onboarding drag and interrupt load on senior staff.
- Impacted: new engineers/TPMs (time-to-productivity), senior engineers/TPMs (interrupts)
- Current cost: ~10–20 repeated questions/week; ~2–4 hours/week of interrupt time across leads
- Failure points: stale docs, links buried, tribal knowledge not captured

**Baseline**
- Time to locate key docs/runbooks: 10–20 minutes per question (new joiner)
- Time spent responding: 5–15 minutes per question (experienced staff)
- Common misses: “latest runbook,” “current system overview,” “current planning cadence”

## 2) Hypothesis
If we deploy a GenAI onboarding Q&A agent constrained to the approved docs hub (RAG + citations), then:
- time-to-answer for common onboarding questions will drop by **50%** within **4 weeks**, and
- onboarding interrupt load on leads will drop by **30%**,
without increasing incorrect guidance above **2%** in weekly sampling.

## 3) Scope (what is / is not included)
**In scope**
- Inputs: docs hub pages only (system overview, runbooks, how-we-work, onboarding checklist)
- Outputs: answers with **citations (links)** to the exact source docs
- Behaviors: “abstain” when uncertain; route to owner when sources missing

**Out of scope**
- Using Slack history as a knowledge base
- Answering questions that require live system access (production status, secrets, credentials)
- Making approvals/decisions (“should we ship” remains human-owned)

## 4) Users and workflow integration (human-in-the-loop)
- Primary users: new joiners, rotating oncall, TPM/Program Ops
- Where it lives: Docs hub page + optional Slack app shortcut (e.g., `/ask-onboarding`)
- Human-in-the-loop:
  - If confidence is low or sources conflict: agent responds with “insufficient source data” and suggests the DRI and doc to update
- Enablement: 20-minute onboarding session + “how to ask good questions” examples

## 5) Guardrails (privacy, security, accuracy)
**Data**
- Allowed classification: internal docs only (approved repos/wiki)
- Prohibited inputs: PII, credentials, access tokens, contracts, customer/advertiser data
- Redaction: automatically strip emails, IDs, secrets (pattern rules)

**Controls**
- Access: only employees in the org; new joiners added via group membership
- Audit/logging: store question, retrieved doc links, prompt version, and answer hash
- Versioning: prompts + retrieval settings stored in repo and changed via PR

**Accuracy requirements**
- Citation-first: every answer includes **2–5 links** to source docs
- No citation → no answer (agent must abstain or ask for doc creation)
- Confidence thresholding:
  - High confidence: answer + citations
  - Medium: answer + “verify with DRI” + citations
  - Low: abstain + route to owner + recommend doc updates
- Failure modes + mitigations:
  - Stale docs → detect “last reviewed” metadata; warn user and route to owner
  - Hallucination risk → enforce citation requirement and abstain when retrieval is weak

**Kill switch**
- Disable if incorrect guidance > 2% for 2 consecutive weeks or prohibited data appears in logs
- Owner authorized: Onboarding Program DRI / Program Ops DRI

## 6) Success metrics (and how we measure)
Limit to a small number of signals: time saved, adoption, quality, and doc health.

| Metric | Baseline | Target | Measurement method | Owner |
|---|---:|---:|---|---|
| Avg time-to-answer (common questions) | 10–20 min | ≤ 5–8 min | user self-report + sampling | Onboarding DRI |
| Lead interrupt time/week | ~2–4 hrs | ≤ 1.5–3 hrs | survey + calendar sampling | Eng lead |
| Adoption rate | 0% | ≥ 60% new joiners use weekly | usage logs | Program Ops |
| Quality (incorrect guidance) | N/A | ≤ 2% | weekly review sample (20 Qs) | Eng lead |
| Doc staleness (Tier 1) | unknown | trend down | staleness report | Docs Hub DRI |

## 7) Rollout plan (time-boxed)
- Pilot group: 3–5 new joiners + 2 mentors
- Duration: 4 weeks
- Enablement/training: 20-minute intro + “approved question types” list
- Feedback loop: weekly 15-minute review:
  - top questions
  - missing docs
  - incorrect/ambiguous answers
- Scale criteria:
  - quality target met for 2 consecutive weeks
  - ≥ 60% of pilot users active weekly
  - measurable reduction in interrupt load
- Exit criteria:
  - quality breach, low adoption (<30%), or inability to enforce citations/guardrails

## 8) Ownership & decision
- Pilot owner (DRI): Onboarding Program DRI
- Partners: Security/Privacy, Docs Hub DRI, Eng lead
- Go/no-go date: end of week 2 (continue, adjust scope, or stop)

## Output format (example)
**Question:** “Where is the runbook for partner event validation failures, and what’s the first 3-step triage?”

**Answer (citation-first):**
1) Open the runbook: `02-operations/runbooks/partner-event-validation.md` (Owner: Data Eng Oncall Lead).  
2) Check “Partner Validation Health” dashboard for `schema_validation_failures` spikes by partner.  
3) If a single partner spikes, confirm schema version + missing required fields (e.g., `adBreakId`) and notify the Partner Integration DRI.  
**Sources:** [Runbook: Partner Event Validation], [Dashboard: Partner Validation Health], [System Overview: Event Ingestion]

**If insufficient source data (abstain):**
“I can’t answer confidently because I could not find an approved runbook or dashboard reference for this component in the docs hub.  
Recommended next step: create/update `02-operations/runbooks/<component>.md` and add it to the ‘Start here’ index.  
Suggested owner to confirm: [DRI / Team].”

