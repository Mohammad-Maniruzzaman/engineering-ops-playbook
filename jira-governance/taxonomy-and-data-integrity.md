# Jira Taxonomy & Data Integrity

## Goal
Make Jira data trustworthy so dashboards, planning, and execution decisions are grounded in reality.

## Required fields (minimum set)
- **Program / Initiative** (e.g., Q1 Planning, Ads Delivery Reliability, Data Quality)
- **Domain / Component** (owned technical area; enables routing and reporting)
- **DRI (Owner)** (single accountable owner)
- **Priority** (defined scale; consistent across teams)
- **Target window** (quarter/month or specific milestone date)
- **Dependency links** (blocked by / blocks)
- **Customer/Stakeholder** (who consumes the outcome)

## Data integrity rules
- No “Unknown/Other” values beyond a small, time-boxed exception process
- Dependencies must be explicit (link issues; avoid hidden spreadsheet-only dependencies)
- Blocked tickets require:
  - blocker type (dependency, resourcing, decision, external)
  - owner + next action + ETA

## Hygiene checks (run weekly)
- Tickets without owners
- Tickets In Progress without updates > 7 days
- Missing program/domain fields
- Blocked tickets with no ETA or next action
- Stale epics (no movement in 14+ days)

## Exception handling
- Exceptions must be documented with a reason and an expiry date
- Track exceptions separately; the goal is to eliminate root causes, not normalize exceptions
