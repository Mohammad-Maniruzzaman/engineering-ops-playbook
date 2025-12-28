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
## How to build these dashboards (practical)

### Shared setup (recommended)
**Prerequisites (data integrity):**
- Standard statuses: Backlog, Ready, In Progress, Blocked, In Review, Done
- Required fields: Program/Initiative, Domain/Component, DRI, Priority, Target window (or Fix Version), Dependency links
- “Meaningful update” captured via one of:
  - issue comments, or
  - a custom field (e.g., “Last Update Summary”), or
  - an Automation rule that stamps a “Last Meaningful Update” date

**Dashboard building approach:**
- Start with **saved filters** (JQL) as the source of truth.
- Build dashboard gadgets from saved filters (Filter Results, Two-Dimensional Filter Statistics, Created vs Resolved, Average Age, Pie Chart).
- Keep each dashboard to **5–8 widgets** maximum.

---

## Dashboard 1: Execution Health (weekly)
**Audience:** Engineering leaders + TPM/Program Ops  
**Cadence:** Weekly (10-minute review)  
**Decisions it should drive:** reduce WIP, fix staleness, unblock dependencies, escalate owners

**Recommended widgets**
1) **Stale In Progress (7+ days without meaningful update)** — Filter Results (top 20)
2) **Blocked items (count)** — Filter Results (top 20)
3) **WIP by Domain/Team** — Two-Dimensional Filter Statistics
4) **Average age of In Progress** — Average Age Chart (or Filter Results sorted by age)
5) **Aging items (>14 days In Progress)** — Filter Results

**Example JQL (adapt field names as needed)**
- WIP:
  - `status = "In Progress" AND resolution = Unresolved`
- Blocked:
  - `status = Blocked AND resolution = Unresolved`
- Aging items (14+ days in progress):
  - `status = "In Progress" AND resolution = Unresolved AND statusCategoryChangedDate <= -14d`
- Staleness (approximation if you do not have a “Last Meaningful Update” field):
  - `status = "In Progress" AND resolution = Unresolved AND updated <= -7d`

> Note: `updated <= -7d` is a rough proxy (any update counts). If you want precision, add a “Last Meaningful Update” field and update it via Automation when a comment is added or a specific field changes.

---

## Dashboard 2: Delivery Throughput (trend)
**Audience:** Eng leads + Finance/Planning partners (optional)  
**Cadence:** Biweekly or monthly review  
**Decisions it should drive:** capacity adjustments, quality/rework fixes, workflow bottleneck removal

**Recommended widgets**
1) **Created vs Resolved** (last 4–8 weeks) — Created vs Resolved Chart
2) **Throughput by week** — Created vs Resolved (or a time-series gadget)
3) **Cycle time proxy** — Average Age for Done items over time (or Control Chart in Jira Software)
4) **Reopen rate** — Filter count of issues reopened

**Example JQL**
- Done last 7 days:
  - `status = Done AND resolved >= -7d`
- Done last 30 days:
  - `status = Done AND resolved >= -30d`
- Reopened items (proxy: moved from Done back to In Progress):
  - If you use Resolution changes, label, or workflow post-function, track via label `reopened` or custom field.
  - Otherwise, maintain a “Reopened” checkbox via Automation when status changes from Done → In Progress.

---

## Dashboard 3: Dependency Risk
**Audience:** Program/TPM + Eng leads  
**Cadence:** Weekly (paired with Execution Health)  
**Decisions it should drive:** clarify DRIs, lock dates, escalate overdue dependencies, re-sequence plans

**Recommended widgets**
1) **Dependencies due in next 14 days** — Filter Results
2) **Overdue dependencies** — Filter Results
3) **Dependencies by owner/team** — Two-Dimensional Filter Statistics
4) **Critical path dependencies** — Filter Results (tagged)

**Implementation tip (lightweight)**
- Track dependencies using:
  - Issue links (blocks/is blocked by), and
  - a date field (e.g., “Needed by”), and
  - a flag for critical path (label `critical_path`)

**Example JQL (requires a date field like “Needed by”)**
- Due soon (next 14 days):
  - `"Needed by" >= startOfDay() AND "Needed by" <= 14d AND status != Done`
- Overdue:
  - `"Needed by" < startOfDay() AND status != Done`
- Critical path:
  - `labels = critical_path AND status != Done`

---

## Dashboard 4: Planning Commitments (quarterly)
**Audience:** Directors/VPs + Program/TPM  
**Cadence:** Weekly during the quarter; heavier review near key dates  
**Decisions it should drive:** scope tradeoffs, milestone confidence, risk burn-down, resourcing moves

**Recommended widgets**
1) **Milestones by date (G/A/R)** — Filter Results grouped by Target date / Fix Version
2) **Scope changes** — simple counts of Added/Removed items (use labels `scope_add`, `scope_remove`)
3) **Top risks + mitigations** — Filter Results from a Risk register project (or label `risk`)
4) **Exec readout link** — link to the latest 1-pager (stored in docs hub)

**Implementation tip (lightweight)**
- Represent commitments as Epics (or a “Milestone” issue type) with a target date.
- Drive G/A/R via a custom field on the milestone item (or labels).


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
