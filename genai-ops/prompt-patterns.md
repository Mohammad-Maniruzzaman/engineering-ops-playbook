# Prompt Patterns (Engineering Ops)

> These are reusable patterns for engineering operations. Always verify outputs, avoid sensitive data, and keep humans in the loop.  
> **Hard rule:** do not invent facts. If sources are missing or conflicting, **abstain** and list the questions needed to proceed.

## Global guardrails (apply to all patterns)
- Use only approved inputs (Jira fields, approved docs hub pages, approved notes).
- Include links/citations to source artifacts whenever possible.
- If uncertainty exists, label it clearly (e.g., “Unconfirmed”).
- Prefer structured output (tables, bullets) over narrative.
- End with a quick **Quality Check** section.

---

## 1) Jira status synthesis (for exec readouts)
**Use case:** Create a weekly 1-page exec readout draft grounded in Jira + dependency register.  
**Inputs (paste or link):**
- Milestone list (with dates + G/A/R if available)
- Top risks + mitigations
- Dependency register (top 5)
- Jira ticket summaries (top 10–20), including links

### Prompt (copy/paste)
You are a Program Ops assistant. Draft a **1-page executive readout** using only the inputs below.  
**Requirements:**
- Be concise, specific, and decision-oriented.
- **Do not invent data.** If missing, list questions under “Missing data / questions.”
- For each bullet, include a **source link** (Jira issue or doc) or label “No source provided.”
- Output must follow this exact structure:

  **1) What changed since last update (max 5 bullets)**  
      **2) Program health (Scope/Schedule/Risks/Dependencies) with 1 sentence each**  
      **3) Key milestones (next 4–6 weeks) table: Date | Milestone | Owner | Confidence**  
      **4) Top risks + mitigations table: Risk | Mitigation | Owner | ETA**  
      **5) Decisions needed / asks (max 5 bullets)**  
      **6) Missing data / questions (if any)**  
      **7) Quality check (see below)**

**Quality check:**
- Are there any claims without a source?
- Are asks time-bound with a named owner?
- Are dependencies explicit with needed-by dates?

**Inputs:**  
[Paste inputs here]

---

## 2) Meeting notes → decisions + actions (decision log hygiene)
**Use case:** Convert raw notes/transcripts into a decision log + action register.  
**Inputs:**
- Raw meeting notes/transcript (paste)
- Attendee list (optional)
- Date/context (optional)

### Prompt (copy/paste)
Extract structured outcomes from the notes below.

**Output requirements:**
1) **Decisions table** with columns: Decision | Why | Owner | Due date | Source quote (1 short excerpt)  
2) **Action items table** with columns: Action | DRI | Due date | Dependency (if any) | Source quote (1 short excerpt)  
3) **Open questions / ambiguities** list: missing owners, unclear dates, unresolved decisions  
4) **Follow-up message draft** (3–6 sentences) requesting missing owners/dates in a crisp way

Rules:
- Do not invent owners or dates. If missing, write “TBD” and flag it.
- Keep quotes under 20 words each.
- Prefer explicit language (“Owner: X by Y”) over summaries.

**Notes:**  
[Paste notes here]

---

## 3) Onboarding Q&A assistant (grounded in SSOT)
**Use case:** Answer onboarding questions using only the docs hub; citation-first; abstain when missing.  
**Inputs:**
- Question
- List of allowed docs (links or pasted excerpts)

### Prompt (copy/paste)
Answer the question using **only** the documentation provided below.

**Output requirements:**
- Provide a direct answer in 3–8 bullets.
- For each bullet, include a **citation** in this format: (Source: <doc title> → <section heading>).
- Quote **section headings** you used (do not quote large passages).
- If the answer is not present, say: “Not found in provided docs,” then propose:
  1) which doc should be created/updated,
  2) suggested owner (role/team),
  3) exact section titles to add.

**Question:**  
[Insert question]

**Allowed documentation:**  
[Insert doc links/excerpts]

---

## 4) Post-incident learning summary (ops-focused)
**Use case:** Create a blameless incident summary with actionable follow-ups and doc updates.  
**Inputs:**
- Incident timeline
- Customer impact summary
- Contributing factors / hypotheses
- Current mitigations
- Links to runbooks/dashboards (if any)

### Prompt (copy/paste)
Generate a blameless, learning-focused incident summary using only the inputs below.

**Output structure:**
1) **Customer impact** (who/what/how long)
2) **Timeline** (5–10 key events with timestamps)
3) **Contributing factors** (group by: People/Process/Tech/External)
4) **What worked / what didn’t**
5) **Corrective actions** table: Action | Owner | Priority (P0/P1/P2) | Due date | Verification method
6) **Docs to update** list: doc/runbook name + section to add/change + owner
7) **Open questions** (if any)
8) **Quality check**

Rules:
- Do not blame individuals; focus on mechanisms.
- Make every corrective action verifiable (how we’ll know it’s fixed).
- If a runbook or doc is missing, explicitly recommend creating one.

**Inputs:**  
[Paste timeline/notes here]
## 5) Ticket refinement (DoR enforcement + acceptance criteria)
**Use case:** Convert a vague intake request into a DoR-ready Jira ticket with clear scope, acceptance criteria, dependencies, and risks—without inventing facts.  
**Inputs:**
- Raw request/intake text (email/Slack note)
- Context links (relevant epic/spec/runbook, if available)
- Known constraints (deadline, compliance, launch freeze, etc.)

### Prompt (copy/paste)
You are a technical program ops assistant. Refine the intake below into a **DoR-ready Jira ticket**.

**Hard rules**
- Do not invent requirements, dates, owners, or technical details.
- If critical info is missing, leave placeholders and list questions.
- Keep scope tight and explicit; list non-goals.

**Output format (exact)**
**Title:**  
**Type:** (Story/Task/Bug)  
**Summary (2–3 sentences):**  
**Problem statement:**  
**Proposed approach (high level):**  
**In scope:**  
**Out of scope:**  
**Acceptance criteria (5–8 bullets, testable):**  
**Success metric (if applicable):**  
**Dependencies:** (team/owner/date if known; otherwise “TBD”)  
**Risks / edge cases:**  
**Rollout / verification:** (how we confirm it worked)  
**Links / sources:** (only what was provided)  
**Missing info / questions (must be time-bound):**

**Quality check**
- Are acceptance criteria testable and unambiguous?
- Is there at least one success metric or verification step?
- Are dependencies explicit with DRIs/dates or clearly marked TBD?

**Intake request:**  
[Paste intake text]

**Available context (links/excerpts):**  
[Paste links/excerpts]
