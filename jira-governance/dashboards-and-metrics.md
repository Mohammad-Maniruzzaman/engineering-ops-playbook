# Dashboards & Metrics (Definitions)

## Principle
Dashboards are decision tools. Each dashboard should answer a specific leadership question and trigger action.

## Shared setup (recommended)
**Data hygiene prerequisites**
- Standard statuses: Backlog, Ready, In Progress, Blocked, In Review, Done
- Required fields: Program/Initiative, Domain/Component, DRI, Priority, Target window (or Fix Version), dependency links
- Staleness measurement: `updated <= -7d` is a proxy; for precision, add a “Last Meaningful Update” field and update it via Automation.

**Build approach**
- Create **saved filters (JQL)** first.
- Build dashboards from filters using a small set of gadgets (Filter Results, Two-Dimensional Filter Statistics, Created vs Resolved, Average Age).
- Keep each dashboard to **5–8 widgets**.

---

## Dashboard 1: Execution Health (weekly)
**Question:** Are we making progress with reliable tracking?

### What it includes
- Staleness rate (tickets not updated in 7 days)
- Blocked count + blocked time
- Work in progress (WIP) by domain/team
- Top aging items (by age or time-in-status)

### How to build it (Jira)
**Recommended widgets**
1) Stale In Progress (7+ days) — Filter Results  
2) Blocked items — Filter Results  
3) WIP by Domain/Team — Two-Dimensional Filter Statistics  
4) Aging In Progress (>14d) — Filter Results (sorted by age)

**Example saved filters (JQL)**
- WIP:
  - `status = "In Progress" AND resolution = Unresolved`
- Blocked:
  - `status = Blocked AND resolution = Unresolved`
- Stale In Progress (proxy):
  - `status = "In Progress" AND resolution = Unresolved AND updated <= -7d`
- Aging In Progress (proxy):
  - `status = "In Progress" AND resolution = Unresolved AND statusCategoryChangedDate <= -14d`

### Decision triggers
- If staleness > 10%: reset ownership, reduce WIP, enforce update SLA.
- If blocked trends up 2 weeks: run dependency review and escalate owners with dates.
- If aging items increase: re-clarify scope/DoD or remove hidden blockers.

### Example (filled): Weekly Execution Health Dashboard
*Illustrative example — numbers and item names are placeholders to demonstrate format and decision triggers.*

**Audience:** Engineering leadership + TPM/Program Ops  
**Cadence:** weekly (10-minute review)  
**Goal:** surface reality quickly—staleness, blockers, and aging work—so decisions happen without additional status meetings.

**Snapshot (Week of Jan 6)**
- **Staleness rate** (In Progress with no update in 7 days): **6%** (target: **<10%**)
- **Blocked items:** **9** (down from 14 last week)
- **Blocked time:** avg **2.1 days** (p75: **4.0 days**)
- **WIP (In Progress):** **37** (watch: **>45**)
- **Aging items** (In Progress > 14 days): **5** (reviewed below)

**Top aging items (actionable list)**

| Item | Program | Domain | Age | Status | Blocker / Next action | Owner | ETA |
|---|---|---|---:|---|---|---|---|
| Partner event schema validation | Platform Integrations | Partner Integrations | 18d | Blocked | Waiting on API field `adBreakId`; confirm delivery date or provide interim stub | A. Khan | Jan 12 |
| Contract tests in CI | Ads Delivery Reliability | Observability & Tooling | 16d | In Progress | Needs code review bandwidth; assign reviewer | Priya | Jan 10 |
| Data pipeline backfill | Data Quality & Validation | Data Pipelines | 15d | In Progress | Risk of rework; confirm data contract version | Miguel | Jan 11 |

**Anti-patterns (avoid gaming)**
- Moving tickets to “Done” without acceptance criteria or artifact links.
- Keeping work “In Progress” to signal activity without meaningful updates.
- Hiding dependencies in meetings/spreadsheets instead of linking issues.

---

## Dashboard 2: Delivery Throughput (trend)
**Question:** Is throughput improving or declining?

### What it includes
- Completed items per week (throughput)
- Cycle time trend (median, p75)
- Reopen rate (quality/rework signal)

### How to build it (Jira)
**Recommended widgets**
1) Created vs Resolved (last 8 weeks) — Created vs Resolved Chart  
2) Done per week — Created vs Resolved or Filter Statistics by week  
3) Cycle time — Jira Software Control Chart (if available) or Average Age proxy  
4) Reopened items — Filter Results (requires tracking approach)

**Example saved filters (JQL)**
- Done last 7 days:
  - `status = Done AND resolved >= -7d`
- Done last 30 days:
  - `status = Done AND resolved >= -30d`

**Reopen rate implementation note**
Reopen is easiest if you stamp a label (e.g., `reopened`) via Automation when status changes from Done → In Progress.

### Decision triggers
- If throughput drops while WIP stays high: reduce concurrency, remove bottlenecks.
- If cycle time p75 worsens: check review SLAs, dependency delays, unclear DoR/DoD.
- If reopen rate rises: tighten acceptance criteria, add validation/contract tests.

---

## Dashboard 3: Dependency Risk
**Question:** Where will dependencies break our plans?

### What it includes
- Dependencies due in next 2–4 weeks
- Overdue dependencies
- Critical path items (high impact + time-bound)

### How to build it (Jira)
**Implementation tip (lightweight)**
Track dependencies with:
- Issue links (blocks/is blocked by)
- A date field (e.g., “Needed by”)
- A critical path label (e.g., `critical_path`)

**Recommended widgets**
1) Due soon (next 14 days) — Filter Results  
2) Overdue dependencies — Filter Results  
3) Dependencies by owner/team — Two-Dimensional Filter Statistics  
4) Critical path dependencies — Filter Results

**Example saved filters (JQL)**
*(Field names are illustrative; adapt to your Jira schema.)*
- Due soon:
  - `"Needed by" >= startOfDay() AND "Needed by" <= 14d AND status != Done`
- Overdue:
  - `"Needed by" < startOfDay() AND status != Done`
- Critical path:
  - `labels = critical_path AND status != Done`

### Decision triggers
- If due-soon items lack DRIs/dates: assign owners immediately.
- If overdue items exist: escalate with a crisp ask (owner + decision + date).
- If critical path grows: re-sequence work or reduce scope.

---

## Dashboard 4: Planning Commitments (quarterly)
**Question:** Are we on track against committed milestones?

### What it includes
- Milestones by date (G/A/R)
- Scope changes (added/removed work)
- Top risks + mitigations

### How to build it (Jira)
**Implementation tip (lightweight)**
- Represent commitments as Epics (or a “Milestone” issue type) with a target date.
- Track status (G/A/R) via a custom field or label.
- Track scope changes via labels (e.g., `scope_add`, `scope_remove`).

**Recommended widgets**
1) Milestones by target date — Filter Results (grouped by date or Fix Version)  
2) Scope changes — Filter counts for `scope_add` and `scope_remove`  
3) Top risks — Filter Results from risk items (or label `risk`)  
4) Link to latest exec readout — link to 1-pager in docs hub

### Decision triggers
- If milestones go Amber/Red: make a scope/resourcing decision and record it.
- If scope adds exceed removes: force explicit tradeoffs.
- If top risks repeat: assign mitigation owners and track to closure.



## Metric notes

### Core metrics (definitions)
- **Staleness rate (%)**  
  **Definition:** % of issues in **In Progress** with **no meaningful update in the last 7 days**.  
  **Intent:** detect hidden WIP and “status churn.”  
  **Formula:** stale_in_progress / total_in_progress

- **WIP (count)**  
  **Definition:** total issues in **In Progress** (optionally segmented by Domain/Team).  
  **Intent:** control concurrency; WIP creep is an early risk signal.

- **Blocked count (count) + Blocked time (days)**  
  **Definition:** number of issues in **Blocked**, and time spent in Blocked per issue (report median + p75).  
  **Intent:** expose dependency friction and decision latency.

- **Cycle time (days) — median + p75**  
  **Definition:** time from **In Progress → Done** (exclude Backlog/Ready wait time).  
  **Intent:** measure delivery experience; p75 surfaces long-tail pain.

- **Throughput (items/week)**  
  **Definition:** count of issues moved to **Done** per week (use a rolling 4-week trend).  
  **Intent:** detect capacity/flow changes without overreacting to noise.

- **Reopen rate (%)**  
  **Definition:** % of completed issues that re-enter **In Progress** within 14 days due to defects/rework.  
  **Intent:** quality/rework signal; used with cycle time, not alone.

### Usage guidelines
- Prefer a small set of stable metrics over frequent changes.
- Use **medians + p75** (avoid averages) to capture real experience.
- Treat metrics as **signals**, not targets; validate data integrity (taxonomy, required fields, and update hygiene) to prevent gaming.

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
