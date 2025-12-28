# Single Source of Truth (SSOT) Structure

## Objective
Create a durable, searchable documentation hub that reduces repeated questions, speeds onboarding, and ensures critical operational knowledge remains current.

## Core rules
- Every critical doc has an **Owner (DRI)** and a **Review cadence**.
- If it is not discoverable in the hub, it does not exist.
- Decisions and operational learnings update docs as part of closure (no “optional” documentation debt).

## Recommended hub structure
- `00-start-here/`
  - `index.md` (what this system is, how to navigate)
  - `glossary.md`
  - `how-we-work.md` (cadence, comms, decision logs)
- `01-architecture/`
  - `system-overview.md`
  - `service-catalog.md`
  - `architecture-specs/` (one spec per system/change)
- `02-operations/`
  - `runbooks/`
  - `oncall/` (if applicable)
  - `incident-reviews/`
- `03-product-and-program/`
  - `roadmap.md`
  - `planning-artifacts/`
  - `dependency-register.md`
- `04-onboarding/`
  - `30-60-90.md`
  - `training-plan.md`
  - `first-week-checklist.md`

## Ownership model
- Hub Owner (DRI): responsible for IA, quality bar, and staleness reporting
- Domain Owners: responsible for their folder content and review cadence
- Contributors: create/update docs via PRs using templates

---

## Example (filled): “Start here” index

*Illustrative example — names and systems are placeholders.*

### What this hub is
This hub is the single source of truth for Ads Engineering execution artifacts: architecture specs, runbooks, onboarding, planning cadence, and decision records.

### If you are new
1) Read `00-start-here/how-we-work.md` (cadence + decision logging)  
2) Read `01-architecture/system-overview.md` (how the system fits together)  
3) Follow the `04-onboarding/first-week-checklist.md`  

### If you are shipping changes
- Create an `01-architecture/architecture-specs/<date>-<change>.md`
- Add links in the weekly update + decision log
- Update the relevant runbook if operational behavior changes

### Quality bar
- Every doc has: owner, last reviewed date, and links to relevant artifacts
- Anything stale is flagged weekly and assigned for refresh
