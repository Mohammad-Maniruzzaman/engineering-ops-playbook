# Prompt Patterns (Engineering Ops)

> Note: These are patterns. Always verify outputs, avoid sensitive data, and keep humans in the loop.

## 1) Jira status synthesis (for exec readouts)
**Input:** Ticket summaries, milestones, risks, dependencies  
**Prompt:**
"Summarize program status for an executive readout. Use: What changed, current health (scope/schedule/risks/deps), top 3 risks with mitigations, decisions needed. Be concise and specific. Do not invent data; if missing, list questions."

## 2) Meeting notes -> decisions + actions
**Input:** Raw notes/transcript  
**Prompt:**
"Extract decisions, owners, and due dates. Then extract action items with DRIs and deadlines. Output in two tables. Flag ambiguities and missing owners."

## 3) Onboarding Q&A assistant (grounded in SSOT)
**Input:** Links or excerpts from the SSOT  
**Prompt:**
"Answer the question using only the provided documentation. Quote the section titles you used. If the answer is not in the docs, say so and propose what doc should be created/updated."

## 4) Post-incident learning summary (ops-focused)
**Input:** Incident timeline and contributing factors  
**Prompt:**
"Generate a learning-focused summary: customer impact, timeline, contributing factors, what worked, what did not, concrete follow-ups with owners, and which docs/runbooks should be updated. Keep tone blameless and actionable."
