# Architecture Spec Template

## 1) Summary (2–3 sentences)
What are we building/changing, and why now?

## 2) Problem statement
What problem does this solve (user/business/operational)?

## 3) Goals / non-goals
- Goals:
- Non-goals:

## 4) Current state
Brief description + links to current diagrams/docs.

## 5) Proposed design
- Components involved:
- Data flow (high level):
- Key interfaces / contracts:
- Observability (logs/metrics/traces):
- Failure modes and mitigations:

## 6) Rollout plan
- Milestones:
- Backward compatibility:
- Migration steps (if any):
- Rollback plan:

## 7) Risks + open questions
- Risks:
- Open questions:

## 8) Ownership
- DRI:
- Reviewers:
- Last updated:

---

## Example (filled)

*Illustrative example — systems and names are placeholders.*

## 1) Summary (2–3 sentences)
We will standardize event schema validation for partner ad integrations to reduce late-cycle integration defects and improve delivery predictability. This change adds contract tests in CI and a versioned schema registry reference used by ingestion.

## 2) Problem statement
Partner integrations frequently fail during end-to-end validation due to schema drift and undocumented field changes. This causes rework, delays, and noisy coordination across teams.

## 3) Goals / non-goals
- Goals:
  - Catch schema drift earlier via automated contract tests
  - Provide a single authoritative schema reference
  - Reduce integration defect rate and stabilize rollout timelines
- Non-goals:
  - Rewriting ingestion pipeline
  - Building a new platform-wide schema registry (we will reference the existing one)

## 4) Current state
Schema validation happens late in staging; issues are discovered during final integration windows. No consistent contract test suite exists for partner events.

## 5) Proposed design
- Components involved:
  - CI pipeline (contract test stage)
  - Partner event schema (versioned)
  - Ingestion validation module
- Key interfaces / contracts:
  - `adBreakId` required for partner events (v2)
  - Version header `schemaVersion`
- Observability:
  - Metric: `schema_validation_failures` (by partner)
  - Log: validation error with missing fields + schemaVersion
- Failure modes and mitigations:
  - Missing required field → fail fast in CI; block release until corrected
  - Partial rollout drift → allow dual read v1/v2 during migration window

## 6) Rollout plan
- Jan 10: add contract tests to CI for top partners
- Jan 20: staging validation enforced (warn-only for 1 week)
- Feb 3: production enforcement + monitoring dashboard live
Rollback: disable enforcement flag; maintain logging for investigation

## 7) Risks + open questions
- Risk: partner teams need time to adopt v2 → mitigation: migration window + tooling
- Open question: exact set of required fields by partner category (confirm by Jan 8)

## 8) Ownership
- DRI: Mohammad
- Reviewers: Platform Eng Lead, Data Eng Lead
- Last updated: Jan 6
