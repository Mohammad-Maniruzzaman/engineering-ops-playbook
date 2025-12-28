# Quarterly Planning Template

## Purpose
Align outcomes, commitments, and capacity for the quarter with clear milestones, dependencies, and decision triggers—so execution is predictable and tradeoffs are explicit.

## How to use (recommended)
- Keep this doc to **2–3 pages**.
- Define **2–3 outcomes** (measurable), then limit commitments to what supports them.
- Every commitment must have: **DRI + target date + success metric + dependencies + risks**.
- If new work is added mid-quarter, record it as a **scope add** with an explicit tradeoff.

---

## 1) Outcomes (what success looks like)
Write outcomes as measurable statements (not activities).

| Outcome | Metric / Target | Why it matters (business/program) | Owner (DRI) |
|---|---|---|---|
| O1 |  |  |  |
| O2 |  |  |  |
| O3 (optional) |  |  |  |

---

## 2) Commitments (what we will deliver)
List only the initiatives required to achieve the outcomes.

| Initiative / Epic | Owner (DRI) | Why now (1 sentence) | Milestones (date + deliverable) | Success metric | Confidence (H/M/L) |
|---|---|---|---|---|---|
|  |  |  |  |  |  |

**Milestone format (recommended):**  
- **[Date]** — **[Deliverable]** — (G/A/R)

---

## 3) Capacity & constraints (assumptions)
Be explicit so leadership understands tradeoffs.

**Capacity**
- Team size / availability assumptions:
- Planned focus allocation (optional): e.g., Delivery 70% / Reliability 20% / Support 10%

**Constraints**
- Known constraints (holidays, hiring gaps, launch freezes):
- Non-negotiables (reliability, compliance, contractual):

---

## 4) Dependencies (top items only)
Track the top dependencies here; the full list lives in the dependency register.

| Dependency | Blocking milestone | Owner (DRI) | Needed by | Status | Escalation trigger | Link |
|---|---|---|---:|---|---|---|
|  |  |  |  |  |  |  |

---

## 5) Risks & mitigations (top risks only)
| Risk | Impact | Likelihood (H/M/L) | Mitigation (specific) | Owner | ETA |
|---|---|---|---|---|---:|
|  |  |  |  |  |  |

---

## 6) Decisions needed (time-bound)
List only decisions that must be made to keep the plan credible.

| Decision | Why it’s needed | Options (A/B) | Owner | By date |
|---|---|---|---|---:|
|  |  |  |  |  |

---

## 7) Execution & communications
**Cadence**
- Weekly exec readout: [Day/time] — owner: [Name]
- Weekly execution health review (Jira): [Day/time] — owner: [Name]
- Dependency review: [Day/time] — owner: [Name]

**Channels**
- Slack channel(s):
- DLs:
- Stakeholders / partners:

---

# Example (filled)
*Illustrative example — names, dates, and programs are placeholders.*

## 1) Outcomes
| Outcome | Metric / Target | Why it matters (business/program) | Owner (DRI) |
|---|---|---|---|
| O1: Improve delivery predictability for integrations | p75 cycle time ≤ 12 days (from 15), staleness < 10% | Fewer surprise slips; reduces leadership escalation and status churn | TPM (Mohammad) |
| O2: Reduce integration defects discovered late | Reopen rate < 5%; schema validation failures < 0.5% | Less rework near launch; better partner experience | Eng Lead (Priya) |

## 2) Commitments
| Initiative / Epic | Owner (DRI) | Why now (1 sentence) | Milestones (date + deliverable) | Success metric | Confidence |
|---|---|---|---|---|---|
| Standardize partner event validation (v2) | Priya | Contract drift is driving late-cycle failures | Jan 20 — E2E validation in staging (G); Feb 3 — prod enforcement (A) | validation failures < 0.5% | M |
| Execution hygiene rollout (Jira + cadence) | Mohammad | Tracking is inconsistent across domains | Jan 10 — taxonomy + dashboards live (G); Jan 24 — staleness < 10% (G) | staleness < 10%; WIP < 45 | H |
| Reporting: top 3 metrics surfaced in exec readout | DS Lead | Leadership needs consistent signal | Jan 18 — metrics spec agreed (G); Feb 10 — dashboard live (G) | weekly readout includes top 3 metrics | H |

## 3) Capacity & constraints
**Capacity**
- Team assumes 8 engineers, 1 TPM; 15% time reserved for support/oncall load.
**Constraints**
- Hiring backfill expected mid-quarter; limited reviewer bandwidth weeks of Jan 6–Jan 17.
- Launch freeze window: Feb 1–Feb 5 (only approved changes).

## 4) Dependencies
| Dependency | Blocking milestone | Owner (DRI) | Needed by | Status | Escalation trigger | Link |
|---|---|---|---:|---|---|---|
| API field `adBreakId` in staging + contract | Jan 20 integration | Platform Eng (Alex) | Jan 12 | At risk | If not confirmed by Jan 10 → escalate to Eng Director with stub option | Jira: PLAT-221 |
| Partner staging credentials | Jan 20 integration | Partner Eng (Sara) | Jan 15 | On track | If not verified by Jan 11 → escalate to Partner Eng manager | Jira: PART-77 |

## 5) Risks & mitigations
| Risk | Impact | Likelihood | Mitigation (specific) | Owner | ETA |
|---|---|---|---|---|---:|
| Upstream API slips | Rollout slips or reduced validation | M | Provide interim stub + parallel validation; de-scope non-critical reporting | Mohammad | Jan 10 |
| Review bottleneck | Cycle time p75 increases | M | 24–48h review SLA + rotating reviewer for critical path | Priya | Jan 10 |

## 6) Decisions needed
| Decision | Why it’s needed | Options (A/B) | Owner | By date |
|---|---|---|---|---:|
| Rollout strategy if API slips | Protect Feb 3 date | A) ship with interim stub B) delay for completeness | Eng Director | Jan 11 |

## 7) Execution & communications
**Cadence**
- Weekly exec readout: Fridays 2pm — owner: Mohammad
- Execution health review: Mondays 10am — owner: Priya
- Dependency review: Wednesdays 11am — owner: Mohammad

**Channels**
- Slack: `#ads-eng-execution`
- Stakeholders: Ads Eng, Platform Eng, Data Science, Partner Eng
