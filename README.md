# Engineering Ops Playbook

Lightweight, practical mechanisms to improve execution quality for Engineering, Data Science, and TPM/Program teams—focused on **truthful tracking, low-overhead planning, durable decisions, and scalable knowledge**.

> **Note for Hiring Managers:** If you are viewing this repository to evaluate Engineering Operations / Technical Program Management skills, this playbook demonstrates my approach to operating-model design, artifact creation, and communication standards.

## Objective (Why this exists)
Technical organizations often pay an “execution tax” as they scale: inconsistent tracking data, high meeting load, unclear ownership, slow onboarding, and decisions that live in chats instead of durable artifacts. The result is predictable business impact—missed timelines, lower engineering throughput, higher operational toil, and slower iteration.

This repository exists to provide a lightweight, reusable **Engineering Operations operating model** (templates + definitions + guardrails) that improves execution speed and clarity **without adding bureaucracy**.

### Scope and Boundaries
This playbook focuses on a small set of mechanisms that drive execution clarity (tracking, planning cadence, docs/onboarding, comms hygiene, and tool pilots). It is designed to be adopted incrementally and adapted to local team needs—prioritizing outcomes and measurable signal over ceremony. The mechanisms here are intentionally minimal: enough structure to scale, not enough to slow teams down.

### Business Outcomes Targeted
- **Faster delivery**: Lower cycle time and fewer blocked days.
- **Higher execution predictability**: Clear milestones, dependencies, and decisions.
- **Lower overhead**: Fewer status meetings and less “where are we?” work.
- **Faster onboarding**: Less tribal knowledge, fewer repeated questions.
- **Safer tool adoption**: Pilots (including GenAI) with guardrails and measurable success criteria.

## What This Playbook Improves
| Problem | Solution |
| :--- | :--- |
| **Jira workflows vary across teams** | Dashboards become reliable via standardized taxonomy. |
| **Planning creates churn/logistics** | Planning focused on clarity and outcomes, not ceremony. |
| **Fragmented/stale documentation** | Onboarding becomes fast and repeatable via SSOT. |
| **Noisy updates** | Decisions become durable and discoverable. |
| **Ungoverned Tool/GenAI pilots** | Pilots run with clear guardrails and success criteria. |

## What’s Inside
- **[Jira governance](./jira-governance/)**  
  Workflow standards, taxonomy/data integrity rules, dashboard definitions.
- **[Planning cadence](./planning-cadence/)**  
  Quarterly planning template, dependency register, executive readout (1 page).
- **[Docs hub + onboarding](./docs-hub-and-onboarding/)**  
  SSOT structure, architecture spec template, 30/60/90 onboarding plan.
- **[Comms hygiene](./comms-hygiene/)**  
  Weekly update template, decision log, Slack/DL hygiene rules.
- **[GenAI ops](./genai-ops/)**  
  Pilot proposal template (guardrails + metrics) and reusable prompt patterns.
- **[Culture events](./events/)**  
  Hack day/demo fair runbook.

## Start Here (Fast Path)
1. **[Jira taxonomy + data integrity](./jira-governance/taxonomy-and-data-integrity.md)**
2. **[Executive readout template](./planning-cadence/exec-readout-template.md)**
3. **[GenAI pilot template](./genai-ops/genai-pilot-template.md)**

## How to Use (Recommended)
1. **Start with Principles:** Read [Operating principles](./00-overview/operating-principles.md).
2. **Pilot:** Select one mechanism for 2–4 weeks (e.g., Jira taxonomy + 1 dashboard + exec readout).
3. **Measure:** Track adoption and outcomes (staleness, cycle time, status churn, onboarding time).
4. **Scale:** Roll out incrementally with a clear ownership model.

## Design Principles
1. **Mechanisms must reduce toil, not create it.**
2. **Truth > Optics:** Tracking must be trusted.
3. **Documentation is a product:** Curated, owned, and used.
4. **Decisions are recorded and searchable.**
5. **Tools are rolled out via pilots** with measurable success criteria and guardrails.

## Opinionated Defaults (Lightweight, Measurable)
These are the defaults I use to keep tracking truthful and overhead low:

*   **Staleness SLA:** Any item in **In Progress** must have an update within **7 days** (otherwise it is not “in progress”).
*   **Blocked Definition:** **Blocked** requires a blocker type + owner + next action + ETA (no exceptions).
*   **Cycle Time Reporting:** Track **median + p75** cycle time (avoid averages).
*   **Dependencies:** Every dependency has a DRI and a “needed by” date; unresolved items within **10 business days** of need are escalated.
*   **Docs as a Product:** Every critical doc has an owner and **quarterly** review cadence; post-incident learnings update docs as part of closure.
*   **Change Management:** Pilot mechanisms for **2–4 weeks** before rollout; delete anything that teams do not use weekly.

---
*This repository contains generic templates and examples only and does not include employer-proprietary information.*
