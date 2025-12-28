# Weekly Update Template (Signal > Noise)

## 1) Headline (1 sentence)
What is the most important update this week?

## 2) Progress (what moved)
- [Item] — outcome/progress — owner
- [Item] — outcome/progress — owner

## 3) Risks / issues (what might break)
- Risk: [what] — mitigation — owner — ETA
- Issue: [what] — next action — owner — ETA

## 4) Dependencies / asks
- Dependency: [what] — needed by — owner
- Ask: [decision/approval/resource] — from [who] — by [when]

## 5) Decisions recorded
- Decision: [what] — date — link to decision log entry

---

## Example (filled)

*Illustrative example — items and dates are placeholders to demonstrate format and clarity.*

## 1) Headline (1 sentence)
We are on track for the Jan 20 integration milestone; Feb 3 rollout is at risk pending an upstream API delivery date.

## 2) Progress (what moved)
- Contract tests added to CI for integration validation — PR merged; coverage at 80% for critical paths — Owner: Priya
- Dependency register cleaned up; all near-term dependencies now have DRIs and “needed by” dates — Owner: Mohammad

## 3) Risks / issues (what might break)
- Risk: Upstream API field `adBreakId` may slip past Jan 12 — mitigation: interim stub + parallel validation window — Owner: Alex — ETA: Jan 12
- Issue: Review bandwidth is a bottleneck for 2 open PRs — next action: assign rotating reviewer + enforce 24–48h SLA for critical-path reviews — Owner: Priya — ETA: Jan 10

## 4) Dependencies / asks
- Dependency: Upstream API field `adBreakId` available in staging — needed by Jan 12 — Owner: Alex
- Ask: Confirm whether we prioritize (A) Feb 3 rollout date or (B) full feature completeness — from Eng Director — by Jan 11

## 5) Decisions recorded
- Decision: De-scope “Reporting Enhancements v2” this quarter to protect critical-path delivery — Jan 6 — link: (add decision log entry)
