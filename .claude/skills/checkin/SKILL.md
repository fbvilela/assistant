---
name: checkin
description: Gentle progress check-in. Especially useful with ADHD mode — non-judgmental follow-up on today's main focus.
aliases:
  - ci
---

# Check-in

A gentle nudge to see how things are going.

## Data Dependencies
- READS: `.assistant/profile.md` (name)
- READS: `.assistant/preferences.md` (adhd_mode)
- READS: `.assistant/state.md` (today's plan, current focus)
- WRITES: `.assistant/state.md` (last check-in time, status update)

## Instructions

### 1. Read State

Read `.assistant/state.md` for today's plan and current focus.
Read `.assistant/preferences.md` for adhd_mode.

### 2. Present Check-in

**If ADHD mode — gentle, one question:**
```
Hey {name}, just checking in.

Your main thing today: {THE Thing from state.md}
How's it going?

1. Done (or close)
2. Working on it
3. Haven't started yet
4. Stuck
```

**If standard mode:**
```
Quick check-in on today's plan:

- THE Thing: {task} — status?
- Would Be Nice: {task} — status?

How are things going?
```

### 3. Respond to Status

**"Done" or "close":**
```
Nice. Want to move to the next thing? (say "what should I work on")
```
Update state.md: mark THE Thing as completed.

**"Working on it":**
```
Good. Keep going. I'll check in again later.
```
Update state.md: last check-in time.

**"Haven't started":**
If ADHD mode:
```
No worries. Want to start with just 2 minutes on it?
Sometimes starting is the hardest part.
```
If standard:
```
Want to start now, or reprioritize? (say "plan my day")
```

**"Stuck":**
```
Let's break it down. What feels too big?
```
Then route to the `/stuck` skill logic.

### 4. Update State

Write to `.assistant/state.md`:
```markdown
## Last Check-in
time: {current time}
response: {done/working/not-started/stuck}
```

---

## ADHD Mode

When `adhd_mode: true` in `.assistant/preferences.md`, adjust check-in behavior:

- If the user reports being in flow or hyperfocus, do NOT suggest switching tasks unless something is genuinely urgent (deadline today, blocking others).
- Acknowledge the cost of interruption: "Switching now costs ~30-45 min to get back into it."
- Default response for "working on it" in flow: "You're in the zone -- keep going. I'll only interrupt for urgent stuff."

---

## Notes

- NEVER guilt-trip. "Haven't started" is information, not failure.
- Keep it to one question. Don't pile on with "also what about X and Y?"
- The 2-minute start technique is from ADHD research — it bypasses initiation paralysis
- If the user seems annoyed by check-ins, note it: suggest adjusting checkin_interval in preferences
