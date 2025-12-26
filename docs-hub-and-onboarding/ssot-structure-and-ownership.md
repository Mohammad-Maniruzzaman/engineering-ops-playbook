# Single Source of Truth (SSOT): Structure + Ownership

## Goal
Make critical technical knowledge discoverable, current, and maintained.

## Recommended taxonomy
- Architecture Specs
- System Diagrams
- APIs / Interfaces
- Runbooks / Ops Guides
- Data Contracts / Event Schemas
- Decision Logs
- Planning Artifacts (roadmaps, milestones)
- Onboarding (learning paths, checklists)

## Ownership model
- Every doc has an **Owner** and **Review Cadence** (e.g., quarterly).
- Teams own the content; Engineering Ops governs structure and hygiene.

## Quality rules
- Architecture specs include: purpose, scope, dependencies, non-goals, risks, rollout.
- Diagrams include: last-updated date, source-of-truth link, owner.
- Runbooks include: triggers, steps, rollback, escalation path.

## Maintenance mechanisms
- Monthly “docs health” audit: stale docs, missing owners, broken links
- Quarterly refresh tied to planning cycles
- Post-incident updates: when incidents expose gaps, docs are updated as part of closure
