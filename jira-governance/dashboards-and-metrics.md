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
