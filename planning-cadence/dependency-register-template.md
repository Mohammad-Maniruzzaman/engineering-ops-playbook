# Dependency Register Template

## Objective
Make cross-team dependencies explicit so plans remain credible. This register is the system of record for **owner (DRI), needed-by date, next action, and escalation triggers**.

## Register
| ID | Dependency (what is needed) | Type (Tech/Decision/Resourcing/External) | Blocking / Blocked (what it impacts) | Why it matters (1 sentence) | Owner (DRI) | Needed by | Confidence (H/M/L) | Status (On track / At risk / Overdue) | Next action (specific) | Escalation trigger | Links |
|---:|---|---|---|---|---|---:|---|---|---|---|---|
| D-001 |  |  |  |  |  |  |  |  |  |  |  |

### Column guidance (keep it crisp)
- **Blocking / Blocked:** name the milestone, epic, or deliverable the dependency affects.
- **Why it matters:** business/program impact (e.g., “blocks integration testing,” “blocks rollout,” “blocks decision”).
- **Confidence:** your belief that it will land by the needed-by date (H/M/L).
- **Escalation trigger:** time-bound (e.g., “If date not confirmed by Jan 10 → escalate to Director”).

---

## Operating rules
- Every dependency has a **single owner (DRI)** and a **Needed by** date.
- “In progress” without a **next action + date** is not a status.
- Status definitions:
  - **On track:** date confirmed and actions in motion
  - **At risk:** date uncertain, confidence Medium/Low, or action stalled
  - **Overdue:** Needed by date passed and dependency not met
- Review cadence: **weekly** (10–15 minutes); twice weekly near key milestones.
- Escalation mechanics:
  - If a dependency is due within **10 business days** and confidence is **M/L**, escalate early with a crisp ask.
  - If due within **5 business days** and still unconfirmed, escalate to leadership with options (re-sequence, stub, de-scope).
  - If **Overdue**, escalate same day and force a decision.

---

## Example (filled)
*Illustrative example — names and dates are placeholders.*

| ID | Dependency (what is needed) | Type | Blocking / Blocked (what it impacts) | Why it matters (1 sentence) | Owner (DRI) | Needed by | Confidence | Status | Next action (specific) | Escalation trigger | Links |
|---:|---|---|---|---|---|---:|---|---|---|---|---|
| D-014 | API field `adBreakId` available in staging + contract documented | Tech | Blocks Jan 20 end-to-end integration; risks Feb 3 rollout | Without this field we cannot validate partner events end-to-end | Alex K. | Jan 12 | L | At risk | Confirm delivery date by Jan 10; provide interim stub if slip | If not confirmed by Jan 10 → escalate to Eng Director with option A/B | Jira: PLAT-221, ADS-884 |
| D-015 | Approve rollout decision: ship with interim stub vs delay | Decision | Blocks Feb 3 rollout go/no-go | Decision required to protect rollout date and set expectations | Eng Director | Jan 11 | M | On track | Present options + recommendation in exec readout | If no decision by Jan 11 → escalate in staff meeting with impact statement | Exec readout link |
| D-016 | Partner test credentials provisioned for staging | External | Blocks validation suite run; delays defect discovery | No credentials means integration defects discovered late | Sara M. | Jan 15 | H | On track | Submit access request + verify login works | If access not verified by Jan 11 → escalate to Partner Eng manager | Jira: PART-77, ADS-901 |

### What “good” looks like
- A dependency becomes actionable when it has: **DRI + needed-by + next action + escalation trigger**.
- Critical items include a **fallback** (stub, re-sequence, de-scope) so leadership can choose quickly.
