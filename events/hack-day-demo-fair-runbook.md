# Demo Fair Runbook (In Person)

## Purpose
Run a repeatable in-person Demo Fair that accelerates learning, improves cross-team visibility, and turns work-in-progress into reusable artifacts—without heavy coordination overhead.

## Outcomes (what success looks like)
- ≥ 80% of teams present at least one demo
- ≥ 60% of attendees provide feedback (QR form)
- ≥ 10 reusable artifacts produced (docs/runbooks/dashboards/code)
- Follow-ups captured with DRIs and due dates within 48 hours

## Scope
**This is**
- A structured forum to showcase progress, learnings, and operational improvements
- A mechanism to reduce status meetings through shared visibility

**This is not**
- A launch gate, design review, or approval meeting
- A performance evaluation event

---

## Roles & responsibilities
- **Event DRI (Program Ops / TPM):** owns timeline, comms, agenda, day-of execution
- **Track lead(s) / MC:** runs the room, timeboxes, keeps energy moving
- **Timekeeper:** enforces 5–7 min demos + 2 min Q&A hard stop
- **Scribe:** captures questions, follow-ups, and owners in shared doc
- **AV/Room support (optional):** mic, projector, adapters, recording (if applicable)

---

## Logistics (in-person specifics)
### Room setup (recommended)
- **Main room + projector** for sequential demos (best for timeboxing and shared attention)
- Seating: classroom or theater, with 1–2 aisles for movement
- **Presenter staging area**: front row reserved for “next up” presenters
- **QR signage** at entry and near screen: agenda, feedback form, artifact hub
- Optional: a side table for networking and “artifact browsing” (printed agenda + QR)

### AV checklist
- Projector + HDMI/USB-C adapters (bring spares)
- Presenter clicker (optional but helpful)
- 1–2 handheld mics if room is large (or a standing mic)
- Power strips at presenter table
- Test Wi-Fi reliability and any VPN needs
- Backup plan: local copies of slides/screenshots in case of network issues

### Materials
- Printed 1-page agenda at entrance (10–20 copies)
- Sticky notes for quick feedback (optional)
- Name tags (optional but helpful if cross-org)

### Check-in flow
- A single “Start Here” slide on screen:
  - QR to agenda/hub
  - QR to feedback form
  - “How to ask questions” guidance (short)
- Scribe confirms the follow-up doc is open and shareable

---

## Timeline & checklist

### T-3 weeks: kickoff + logistics
- Confirm date/time (90–120 minutes) and location
- Reserve room and confirm AV availability
- Define 2–4 themes/tracks (optional; still run as one room)
- Create central hub (single link):
  - Agenda + sign-up
  - Demo submission template
  - Feedback QR
  - Artifact links (live doc)

### T-2 weeks: call for demos
- Send call for demos:
  - 5–7 min demo + 2 min Q&A
  - must include artifact link + one measurable signal (if available)
- Recruit 2–3 anchor demos early

### T-1 week: finalize agenda
- Lock the demo list and timeslots
- Publish agenda with “Next up” ordering
- Confirm each demo includes:
  - what problem it solves
  - before → after
  - artifact link
  - ask / next step (optional)

### T-2 days: dry run (recommended)
- 20–30 min run-through with presenters (optional)
- Test AV, adapters, clicker, and screen share
- Confirm presenters can access required apps/sites

### Day-of: execute
- Room set + check-in slide on screen 15 minutes early
- Run the event timeboxed; scribe captures follow-ups live

### T+1 day: publish artifacts + follow-ups
- Post:
  - artifact link list
  - follow-up register (DRI + due date)
  - quick feedback summary

### T+1 week: impact check
- Follow-up completion rate
- Identify top 3 artifacts to standardize/adopt
- Update the runbook with lessons learned

---

## Demo submission template (for presenters)
- Title:
- Theme (optional): 
- 1-liner (what it solves):  
- Before → After (what changed):  
- Who benefits: 
- Demo steps (2–4 bullets):  
- Artifact link(s): (repo/doc/dashboard)  
- Measured impact (if available): (time saved, cycle time reduced, errors reduced)  
- Ask / next step: (what support you need)

---

## Agenda template (90 minutes, single-room)
1) Welcome + purpose + rules (5 min)  
2) Demos (60–75 min total, timeboxed)  
3) Lightning demos (optional, 10–15 min)  
4) Follow-ups: owners + due dates (10 min)  
5) Close + feedback QR reminder (5 min)

---

## Day-of script (MC)
**Opening (30–60 seconds):**
- “Goal today: share learning and reusable artifacts. This is not a gate.”
- “Demos are 5–7 minutes with 2 minutes Q&A. We’ll timebox hard.”
- “Please scan the QR for the agenda + feedback form. Artifacts live in the hub.”

**Before each demo (10 seconds):**
- “Next up: [Presenter], demoing [Title].”

**After each demo (10–20 seconds):**
- “One question. If you have follow-ups, add them to the doc with your name and a due date.”

**Close (30–60 seconds):**
- “Please take 60 seconds to fill feedback—what to adopt, what to simplify.”
- “Follow-ups and artifact links will be published by tomorrow.”

---

## Timeboxing rules
- Demo: **5–7 minutes max**
- Q&A: **2 minutes max**
- If deeper discussion needed: park it in follow-ups or a post-event breakout

---

## Feedback (QR form)
3 questions only:
1) Most useful demo and why  
2) What should we adopt/scale?  
3) What should we stop doing / simplify?

---

## Output artifacts (publish within 24 hours)
- Final agenda + presenters
- Artifact links list
- Follow-ups register: action | owner | due date | status
- Optional: photos of key slides/whiteboards (if allowed)

---

## Example (filled)
*Illustrative example — placeholders.*

### Sample demo entries
1) **Execution Health Dashboard v1**
   - Before: inconsistent ticket updates; status meetings grew
   - After: weekly dashboard review + staleness SLA
   - Artifact: `/dashboards-metrics/definitions.md`
   - Impact: reduced status meeting time by ~20% (sampling)

2) **Dependency Register + escalation triggers**
   - Before: hidden blockers discovered late
   - After: weekly review with T-10/T-5 escalation triggers
   - Artifact: `/planning-cadence/dependency-register-template.md`

3) **Onboarding Q&A Agent (Docs Hub RAG)**
   - Before: repeated questions + tribal knowledge
   - After: citation-first assistant constrained to docs hub
   - Artifact: `/genai-ops/pilot-proposal-template.md`

### Follow-ups (captured live)
| Action | Owner | Due date | Status |
|---|---|---:|---|
| Add “Last reviewed” metadata to Tier-1 runbooks | Docs Hub DRI | Jan 15 | Open |
| Create Jira automation for “Last Meaningful Update” | Program Ops | Jan 20 | Open |
| Pilot onboarding agent with 3 new joiners | Onboarding DRI | Jan 27 | Open |
