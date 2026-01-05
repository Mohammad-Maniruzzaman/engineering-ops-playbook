# Engineering Ops Playbook

Lightweight, practical mechanisms to improve execution quality for Engineering, Data Science, and TPM/Program teams.

**Core Philosophy:** Truthful tracking, low-overhead planning, durable decisions, and context over control.

> **Note for Hiring Managers:** If you are viewing this repository to evaluate Engineering Operations / Technical Program Management skills, this playbook demonstrates my approach to operating-model design: **high alignment, loose coupling, and clear signal.**

## Objective (Why this exists)
Technical organizations often pay an “execution tax” as they scale: inconsistent tracking data, high meeting load, and decisions that live in transient chats.

This repository provides a lightweight **operating model** to drive execution speed and clarity **without adding bureaucracy**. It focuses on giving teams the *context* they need to move fast, rather than controlling how they work.

### Business Outcomes Targeted
*   **Faster delivery:** Lower cycle time and fewer blocked days.
*   **Higher predictability:** Clear milestones and cross-functional dependency management.
*   **Narrative culture:** Moving from status meetings to durable, asynchronous written updates.
*   **Safer tool adoption:** Pilots (including GenAI) with clear success metrics.

## What This Playbook Improves
| Problem | Solution |
| :--- | :--- |
| **Low visibility into progress** | **High-Fidelity Signal:** Standardized datasets for autonomous decision making. |
| **Planning creates churn** | **Narrative Planning:** Memos and outcomes over slide decks and ceremony. |
| **Fragmented knowledge** | **Scalable Context:** SSOT structure for faster onboarding and less tribal knowledge. |
| **Complex dependencies** | **Integration Clarity:** Clear contracts for cross-functional (Sales/Product) handoffs. |

## What’s Inside
*   **[Jira Signal & Data Health](./jira-governance/)** (`/jira-governance`)
    *   *Goal:* Ensure Jira provides reliable data for decision-making, not just "ticket management."
    *   *Includes:* Taxonomy standards, data integrity rules, health dashboards.
*   **[Planning Cadence](./planning-cadence/)**
    *   *Goal:* High alignment on quarterly outcomes.
    *   *Includes:* Quarterly planning narrative, dependency register, executive memo template.
*   **[Docs Hub + Onboarding](./docs-hub-and-onboarding/)**
    *   *Goal:* Context at scale.
    *   *Includes:* Architecture spec templates, 30/60/90 onboarding plans.
*   **[Comms Hygiene](./comms-hygiene/)**
    *   *Goal:* High-signal, low-noise communication.
    *   *Includes:* Narrative update templates, decision logs (DACI/SPADE), communication contracts.
*   **[GenAI Ops](./genai-ops/)**
    *   *Goal:* Developer productivity and safe experimentation.
    *   *Includes:* Pilot proposal templates (guardrails + metrics) and prompt patterns for TPMs.

## Start Here (High Impact)
1.  **[Operating Principles](./00-overview/operating-principles.md)** – *How we think.*
2.  **[Executive Readout Memo](./planning-cadence/exec-readout-template.md)** – *How we communicate value.*
3.  **[GenAI Pilot Template](./genai-ops/genai-pilot-template.md)** – *How we innovate safely.*

## Opinionated Defaults (The "Rules of the Road")
These are the defaults I use to keep tracking truthful and overhead low:

*   **Staleness SLA:** Truth > Optics. Any item in **In Progress** must have an update within **7 days** or it is flagged as stale.
*   **Blocked Definition:** **Blocked** requires a blocker type + owner + next action + ETA. No "blocked" without context.
*   **Cycle Time:** We track **median + p75** cycle time to understand volatility, not just averages.
*   **Dependencies:** Every dependency has a DRI and a “needed by” date. Unresolved items are escalated **10 days** prior to the need-by date.
*   **Docs as Product:** Every critical doc has an owner and a review cadence.
*   **Pilots:** New tools/processes run for **2–4 weeks** with defined success criteria. If it doesn't add value, we deprecated it.

---
*This repository contains generic templates and examples only and does not include employer-proprietary information.*
