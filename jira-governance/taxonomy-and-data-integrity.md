# Jira Taxonomy & Data Integrity

## Goal
Make Jira data trustworthy so dashboards, planning, and execution decisions are grounded in reality. **Taxonomy** should be just rich enough to route work and produce trustworthy dashboards—no more.

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
---

## Example (filled): Minimal taxonomy that supports reporting without bureaucracy

### Example values (illustrative)
**Program / Initiative**
- Ads Delivery Reliability
- Measurement & Reporting
- Data Quality & Validation
- Onboarding & Enablement
- Platform Integrations

**Domain / Component**
- Playback Ad Insertion
- Experimentation / A-B Testing
- Data Pipelines
- Partner Integrations
- Observability & Tooling

### Example ticket (what “good” looks like)
- **Title:** Validate ad event schema for partner integration
- **Program / Initiative:** Platform Integrations
- **Domain / Component:** Partner Integrations
- **DRI (Owner):** A. Khan
- **Priority:** P1
- **Target window:** Jan 2026
- **Dependencies:** Blocks/Blocked by: API field `adBreakId` (linked ticket)
- **Customer/Stakeholder:** Ads Engineering + Data Science
- **Status:** Blocked
- **Blocker type:** Dependency
- **Next action:** Platform team confirms delivery date + provides interim stub
- **ETA:** Jan 12

### Weekly hygiene query (simple checklist)
- In Progress items with no update in 7 days
- Blocked items missing owner/ETA/next action
- Tickets missing Program/Domain/DRI
- Dependencies due in next 2 weeks without confirmed owner/date

