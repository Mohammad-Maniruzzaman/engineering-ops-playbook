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



## Metric notes (definitions + Jira implementation + interpretation)

> Field names and exact gadgets vary by Jira setup. The patterns below are Jira-native (saved filters + dashboard gadgets) and can be made more precise via Automation or BI when needed.

### 1) Staleness rate (%)
**Definition:** % of issues in **In Progress** with **no meaningful update** in the last 7 days.  
**Business/program signal:** “Are we seeing real progress or status-churn?” Trusted tracking reduces meeting overhead and surprise slips.

**Jira implementation (baseline proxy)**
- Saved filter:  
  `status = "In Progress" AND resolution = Unresolved`
- Saved filter (stale proxy):  
  `status = "In Progress" AND resolution = Unresolved AND updated <= -7d`
- Dashboard gadgets:
  - “Filter Results” (list stale issues)
  - “Filter Count” (stale count) + “Filter Count” (WIP count)

**Example calculation (manual % using counts)**
- WIP count = 37 (from WIP filter)
- Stale count = 2 (from stale filter)
- Staleness rate ≈ 2 / 37 = 5.4%

**Leader interpretation**
- Rising staleness usually means unclear ownership, hidden blockers, or too much WIP.
- Action: reassign DRIs, reduce WIP, enforce update hygiene, or re-scope work.

**Precision note**
`updated <= -7d` counts any update (including status toggles). For “meaningful update,” add a field like **Last Meaningful Update** and stamp it via Automation when a comment is added or a status note field is updated.

---

### 2) WIP (count)
**Definition:** number of issues in **In Progress** (optionally by domain/team).  
**Business/program signal:** WIP is a leading indicator of throughput and predictability; high WIP increases cycle time and coordination cost.

**Jira implementation**
- Saved filter:  
  `status = "In Progress" AND resolution = Unresolved`
- Dashboard gadgets:
  - “Filter Count” (WIP)
  - “Two-Dimensional Filter Statistics” (WIP by Domain x Team)

**Example calculation**
- WIP = 37 overall; Domain split shows: Integrations 14, Data 9, Tooling 8, Other 6.

**Leader interpretation**
- If WIP grows but throughput is flat: you likely have bottlenecks (review/approval, dependencies).
- Action: cap WIP, improve review SLAs, break work into smaller units.

---

### 3) Blocked count + Blocked time (days)
**Definition:** count of issues in **Blocked** plus time spent blocked (median + p75).  
**Business/program signal:** dependency friction and decision latency; blocked time directly translates to delivery slip risk.

**Jira implementation**
- Saved filter:  
  `status = Blocked AND resolution = Unresolved`
- Dashboard gadgets:
  - “Filter Results” (blocked list, includes owner/ETA fields)
  - “Average Age” (proxy for blocked duration if you keep items in Blocked)
- Better (if available): Jira Software reports or marketplace apps that compute time-in-status.

**Example calculation**
- Blocked items = 9
- Of those, 3 have ETA > 10 business days and are on critical path → escalation candidate.

**Leader interpretation**
- Blocked count trending up for 2+ weeks indicates cross-team misalignment or missing DRIs.
- Action: dependency review, explicit owner/date, escalation with crisp asks.

---

### 4) Cycle time (days) — median + p75
**Definition:** time from **In Progress → Done**.  
**Business/program signal:** delivery efficiency and predictability; p75 reflects the “real experience” for long-tail work.

**Jira implementation**
- Best (Jira Software): Control Chart / Cycle Time report (if enabled for boards)
- Baseline (proxy): “Average Age” for Done items in a time window is imperfect; prefer Jira Software report or export to BI.

**Example interpretation**
- Median stable at ~6 days, p75 increases from 11 → 15 days = long-tail worsening.
- Likely causes: dependency delays, review bottlenecks, unclear DoR/DoD, oversized tickets.

**Leader interpretation**
- If p75 worsens while throughput is stable: you are finishing easy work while hard work ages.
- Action: break up large items, prioritize clearing blockers, enforce review SLAs, reduce WIP.

---

### 5) Throughput (items/week)
**Definition:** count of issues moved to **Done** per week (use 4-week rolling trend).  
**Business/program signal:** capacity/flow. Sustained improvements correlate with faster delivery and lower execution overhead.

**Jira implementation**
- Saved filter (Done, last 7 days):  
  `status = Done AND resolved >= -7d`
- Gadget:
  - “Created vs Resolved” (trend)
  - “Filter Count” (weekly done)

**Example interpretation**
- Throughput dips from 44 → 38 for two weeks while WIP increases = bottleneck or scope inflation.
- Action: address constraints (review bandwidth, dependency dates), reduce concurrent work.

---

### 6) Reopen rate (%)
**Definition:** % of completed issues that re-enter **In Progress** within 14 days due to defects/rework.  
**Business/program signal:** quality/rework tax; high reopen rate creates churn, delays, and erodes predictability.

**Jira implementation options**
- Best: track a “Reopened” custom field or label via Automation when status transitions **Done → In Progress**.
- Then:
  - Saved filter (reopened, last 14 days):  
    `labels = reopened AND updated >= -14d`
  - Saved filter (done, last 14 days):  
    `status = Done AND resolved >= -14d`
  - Use counts to compute %.

**Example calculation**
- Done last 14 days = 120
- Reopened last 14 days = 8
- Reopen rate ≈ 8 / 120 = 6.7%

**Leader interpretation**
- Rising reopen rate often means weak acceptance criteria, missing validation, or rushed reviews.
- Action: tighten DoD, add contract tests, improve review quality and release gates.

---

### Usage guidance (how leaders should use metrics)
- Metrics are **signals**, not targets. Use them to ask: “What changed in the system?”
- Always interpret metrics together (e.g., WIP + throughput + cycle time).
- When a metric worsens, respond with a **mechanism change** (WIP cap, review SLA, dependency escalation), not more meetings.
ets instead of linking issues.
