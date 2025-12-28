# Dashboards & Metrics (Definitions)

## Principle
Dashboards are decision tools. Each dashboard should answer a specific leadership question.

## Dashboard 1: Execution Health (weekly)
**Question:** Are we making progress with reliable tracking?
- Staleness rate (tickets not updated in 7 days)
- Blocked count + blocked time
- Work in progress (WIP) by domain/team
- Top aging items (by cycle time)

## Dashboard 2: Delivery Throughput (trend)
**Question:** Is throughput improving or declining?
- Completed items per week (throughput)
- Cycle time trend (median, p75)
- Reopen rate (quality/rework signal)

## Dashboard 3: Dependency Risk
**Question:** Where will dependencies break our plans?
- Dependencies due in next 2–4 weeks
- Overdue dependencies
- Critical path items (high impact + time-bound)

## Dashboard 4: Planning Commitments (quarterly)
**Question:** Are we on track against committed milestones?
- Milestones by date (G/A/R)
- Scope changes (added/removed work)
- Top risks + mitigations

## Metric notes
- Prefer a small set of stable metrics over frequent changes.
- Use p75 cycle time (not averages) to capture the real experience.
- Treat metrics as signals, not targets; prevent gaming through data integrity rules.
---
## Example (filled): Weekly Execution Health Dashboard

*Illustrative example — numbers and item names are placeholders to demonstrate format and decision triggers.*

**Audience:** Engineering leadership + TPM/Program Ops  
**Cadence:** weekly (10-minute review)  
**Goal:** surface reality quickly—staleness, blockers, and aging work—so decisions happen without additional status meetings.

### Snapshot (Week of Jan 6)
- **Staleness rate** (In Progress with no update in 7 days): **6%** (target: **<10%**)
- **Blocked items:** **9** (down from 14 last week)
- **Blocked time:** avg **2.1 days** (p75: **4.0 days**)
- **WIP (In Progress):** **37** (watch: **>45**)
- **Aging items** (In Progress > 14 days): **5** (reviewed below)

### Top aging items (actionable list)
| Item | Program | Domain | Age | Status | Blocker / Next action | Owner | ETA |
|---|---|---|---:|---|---|---|---|
| Partner event schema validation | Platform Integrations | Partner Integrations | 18d | Blocked | Waiting on API field `adBreakId`; confirm delivery date or provide interim stub | A. Khan | Jan 12 |
| Contract tests in CI | Ads Delivery Reliability | Observability & Tooling | 16d | In Progress | Needs code review bandwidth; assign reviewer | Priya | Jan 10 |
| Data pipeline backfill | Data Quality & Validation | Data Pipelines | 15d | In Progress | Risk of rework; confirm data contract version | Miguel | Jan 11 |

### Decision triggers
- If **staleness > 10%**: reset ownership, reduce WIP, and enforce the update SLA.
- If **blocked items trend up** for 2 weeks: run a dependency review and escalate owners with dates.
- If **p75 cycle time worsens**: check for hidden WIP, unclear DoR/DoD, or review bottlenecks.

### Anti-patterns (avoid gaming)
- Moving tickets to “Done” without acceptance criteria or artifact links.
- Keeping work “In Progress” to signal activity without meaningful updates.
- Hiding dependencies in meetings/spreadsheets instead of linking issues.
