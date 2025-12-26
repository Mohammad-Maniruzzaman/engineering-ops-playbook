# Jira Workflow Standards

## Purpose
Standardize workflows so tracking data is reliable, comparable across teams, and usable for decision-making.

## Standard status definitions
- **Backlog**: approved work, not yet committed to a sprint/cycle
- **Ready**: meets Definition of Ready (DoR) and can be pulled
- **In Progress**: actively being worked
- **Blocked**: progress stopped; blocker recorded with owner + ETA
- **In Review**: awaiting review/approval
- **Done**: meets Definition of Done (DoD) and is shipped/accepted

## Definition of Ready (DoR)
Ticket must include:
- Clear problem statement and expected outcome
- DRI (owner) and target window
- Dependencies documented (if any)
- Acceptance criteria and/or success metric
- Link to relevant spec or note (if needed)

## Definition of Done (DoD)
- Acceptance criteria met
- Stakeholders notified (as applicable)
- Links to docs/runbooks updated
- Post-implementation notes recorded (if applicable)

## Operating rules
- No ticket stays **In Progress** without update > 7 days
- **Blocked** tickets must include: blocker type, owner, next action, ETA
- Teams use the same required fields (see taxonomy)
- Status changes are meaningful: do not use statuses to “look green”
