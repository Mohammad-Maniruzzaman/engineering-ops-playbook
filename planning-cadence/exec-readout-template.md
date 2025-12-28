# Executive Readout (1 page)

**Purpose:** Drive decisions and unblock execution. This is not a status dump.  
**Rule of thumb:** If a line does not change a decision, priority, or resourcing, delete it.

---

## 1) What changed since last update (delta only)
- [Change 1: what changed + why it matters]
- [Change 2: what changed + impact/risk]
- [Optional: new risk or dependency surfaced]

## 2) Program health (RAG + why)
- **Scope:** [G/A/R] — [What changed in scope; what was added/removed and why]
- **Schedule:** [G/A/R] — [Are key milestones still credible? what moved?]
- **Risks:** [G/A/R] — [Top risk + mitigation + owner]
- **Dependencies:** [G/A/R] — [Top dependency + specific ask + date]

## 3) Key milestones (next 4–6 weeks)
- [Date] — [Milestone] — Owner: [Name] — Status: [On track / At risk] — Notes: [1 line]
- [Date] — [Milestone] — Owner: [Name] — Status: [On track / At risk] — Notes: [1 line]

## 4) Top risks + mitigations (limit to 2–3)
1. [Risk] — Mitigation — Owner — ETA — Escalation needed? [Y/N]
2. [Risk] — Mitigation — Owner — ETA — Escalation needed? [Y/N]

## 5) Decisions needed / asks (make these crisp)
- **Decision needed:** [What decision] — Owner: [Name] — Needed by: [Date] — Options: [A/B] — Recommendation: [A]
- **Ask:** [What you need] — From: [Who] — Needed by: [Date] — If not met: [impact]

---

# Example (filled)

## 1) What changed since last update (delta only)
- External dependency slipped by 2 weeks; we re-sequenced work to protect the Jan 20 milestone, but Feb 3 delivery is now at risk.
- We reduced scope: removed low-impact reporting enhancement to stay within capacity (revisit next quarter).

## 2) Program health (RAG + why)
- **Scope:** Amber — De-scoped “Reporting Enhancements v2” to protect critical-path delivery.
- **Schedule:** Amber — Jan 20 milestone still credible; Feb 3 milestone depends on upstream API availability by Jan 12.
- **Risks:** Amber — Risk: integration defects discovered late in the cycle. Mitigation: add contract tests + daily integration window; Owner: Priya; ETA: Jan 10.
- **Dependencies:** Red — Need upstream API field `adBreakId` by **Jan 12**. Ask: confirm delivery date or provide interim stub; Owner: Platform Eng (DRI: Alex).

## 3) Key milestones (next 4–6 weeks)
- Jan 10 — Contract tests in CI — Owner: Priya — Status: On track — Notes: PR in review
- Jan 20 — End-to-end integration complete — Owner: Mohammad — Status: On track — Notes: requires API field by Jan 12
- Feb 3 — Production rollout — Owner: Mohammad — Status: At risk — Notes: depends on upstream delivery + validation

## 4) Top risks + mitigations (limit to 2–3)
1. Upstream API field delayed — Mitigation: interim stub + parallel validation — Owner: Alex — ETA: Jan 12 — Escalation needed? Y
2. Late-cycle integration defects — Mitigation: contract tests + daily integration window — Owner: Priya — ETA: Jan 10 — Escalation needed? N

## 5) Decisions needed / asks (make these crisp)
- **Decision needed:** If upstream API slips past Jan 12, do we (A) delay Feb 3 rollout or (B) ship with interim stub? Owner: Eng Director — Needed by: Jan 11 — Recommendation: B (protect rollout; swap to final field post-launch).
- **Ask:** Confirm upstream API delivery date and DRI for support during validation — From: Platform Eng Lead — Needed by: Jan 10 — If not met: Feb 3 rollout likely slips.
