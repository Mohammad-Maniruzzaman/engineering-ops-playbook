# Engineering Ops Playbook

Lightweight, practical mechanisms to improve execution quality for Engineering, Data Science, and TPM/Program teams—focused on **truthful tracking, low-overhead planning, durable decisions, and scalable knowledge**.

If you are hiring for Engineering Operations / Program Management roles, this repo is intended to demonstrate operating-model design and clear communication artifacts.
## Objective (why this exists)
Technical organizations often pay an “execution tax” as they scale: inconsistent tracking data, high meeting load, unclear ownership, slow onboarding, and decisions that live in chats instead of durable artifacts. The result is predictable business impact—missed timelines, lower engineering throughput, higher operational toil, and slower iteration.

This repository exists to provide a lightweight, reusable **Engineering Operations operating model** (templates + definitions + guardrails) that improves execution speed and clarity **without adding bureaucracy**.

### Scope and boundaries
This playbook focuses on a small set of mechanisms that drive execution clarity (tracking, planning cadence, docs/onboarding, comms hygiene, and tool pilots). It is designed to be adopted incrementally and adapted to local team needs—prioritizing outcomes and measurable signal over ceremony. The intent is to reduce execution overhead while improving truth and decision velocity. The mechanisms here are intentionally minimal: enough structure to scale, not enough to slow teams down.

### Business outcomes this playbook targets
- **Faster delivery**: lower cycle time and fewer blocked days
- **Higher execution predictability**: clear milestones, dependencies, and decisions
- **Lower overhead**: fewer status meetings and less “where are we?” work
- **Faster onboarding**: less tribal knowledge, fewer repeated questions
- **Safer tool adoption (including GenAI)**: pilots with guardrails and measurable success criteria

## What this playbook improves
- Jira workflows/fields vary across teams → dashboards become unreliable
- Planning cycles create churn/logistics overhead instead of clarity
- Documentation is fragmented/stale → onboarding is slow and repetitive
- Updates are noisy → decisions are not durable or discoverable
- Tool pilots (including GenAI) lack guardrails and success criteria

## What’s inside (clickable)
- **Jira governance** → [jira-governance/](./jira-governance/)  
  Workflow standards, taxonomy/data integrity rules, dashboard definitions
- **Planning cadence** → [planning-cadence/](./planning-cadence/)  
  Quarterly planning template, dependency register, executive readout (1 page)
- **Docs hub + onboarding** → [docs-hub-and-onboarding/](./docs-hub-and-onboarding/)  
  SSOT structure, architecture spec template, 30/60/90 onboarding plan
- **Comms hygiene** → [comms-hygiene/](./comms-hygiene/)  
  Weekly update template, decision log, Slack/DL hygiene rules
- **GenAI ops** → [genai-ops/](./genai-ops/)  
  Pilot proposal template (guardrails + metrics) and reusable prompt patterns
- **Culture events** → [events/](./events/)  
  Hack day/demo fair runbook


## Start here (fast path)
- [Jira taxonomy + data integrity](./jira-governance/taxonomy-and-data-integrity.md)
- [Executive readout template](./planning-cadence/exec-readout-template.md)
- [GenAI pilot template](./genai-ops/genai-pilot-template.md)

## How to use (recommended)
1) Start with [Operating principles](./00-overview/operating-principles.md).
2) Pilot one mechanism for 2–4 weeks (e.g., Jira taxonomy + 1 dashboard + exec readout).
3) Measure adoption + outcomes (staleness, cycle time, status churn, onboarding time).
4) Roll out incrementally with a clear ownership model.

## Design principles
- Mechanisms must reduce toil, not create it.
- Truth > optics: tracking must be trusted.
- Documentation is a product: curated, owned, and used.
- Decisions are recorded and searchable.
- Tools are rolled out via pilots with measurable success criteria and guardrails.

## Opinionated defaults (lightweight, measurable)
These are the defaults I use to keep tracking truthful and overhead low:
- **Staleness SLA:** any item in **In Progress** must have an update within **7 days** (otherwise it is not “in progress”).
- **Blocked definition:** **Blocked** requires a blocker type + owner + next action + ETA (no exceptions).
- **Cycle time reporting:** track **median + p75** cycle time (avoid averages).
- **Dependencies:** every dependency has a DRI and a “needed by” date; unresolved items within **10 business days** of need are escalated.
- **Docs as a product:** every critical doc has an owner and **quarterly** review cadence; post-incident learnings update docs as part of closure.
- **Change management:** pilot mechanisms for **2–4 weeks** before rollout; delete anything that teams do not use weekly.

## Notes
This repository contains generic templates and examples only and does not include employer-proprietary information.
