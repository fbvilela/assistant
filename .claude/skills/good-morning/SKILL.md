---
name: good-morning
description: Morning briefing and daily planning. Use when the user wants to start their day or get an overview.
aliases:
  - gm
---

# Good Morning

Start the day with a briefing and a plan.

## Data Dependencies
- READS: `.assistant/profile.md` (name, weather_location)
- READS: `.assistant/preferences.md` (adhd_mode, task_structure)
- READS: `.assistant/integrations.md` (calendar config)
- READS: `.assistant/state.md` (carry-over from yesterday)
- READS: `01-Projects/` (active project next actions)
- READS: `02-Areas/` (area tasks)
- READS: `Daily Plans/` (yesterday's plan if exists)
- WRITES: `.assistant/state.md` (today's plan)
- WRITES: `Daily Plans/YYYY-MM-DD.md` (today's daily plan)

## Instructions

### 1. Read Context

Read `.assistant/profile.md` for name and weather_location.
Read `.assistant/preferences.md` for adhd_mode and task_structure.
Read `.assistant/integrations.md` for calendar configuration.
Read `.assistant/state.md` for carry-over items.

### 2. Calendar

Check `.assistant/integrations.md` for calendar type.

If `type: apple-calendar` and tool is available:
```bash
icalBuddy -f -n -ea -nc -ps "| : |" -po "title,datetime" eventsToday 2>/dev/null
```

If no calendar configured, skip this section silently.

### 3. Check Carry-Over from Yesterday

Read `.assistant/state.md` for carry-over items. If there are tasks in the Carry Over section:
1. Include them in the briefing under "Carry Over"
2. These will be incorporated into today's plan in step 6

### 4. Weather

Read weather_location from profile.
```bash
curl -s "wttr.in/{weather_location}?format=%t+%C" 2>/dev/null || echo "Weather unavailable"
```

### 5. Present Briefing

```
Good morning, {name}.

## Today's Schedule
- 9:00 AM — Team standup
- 2:00 PM — Client call
(or "Calendar is clear today" / or skip if no calendar)

## Carry Over
- {items from state.md carry-over section}
(or skip if none)

## Active Projects
{next actions from 01-Projects/ and 02-Areas/}

## {weather_location}
22°C, Partly cloudy
```

### 6. Set Today's Plan

Check preferences for task_structure.

**If ADHD mode (3-things structure):**
```
Let's set your 3 things for today.

What's THE Thing? (the one thing that matters most today)
```

Wait for answer, then:
```
What Would Be Nice to also get done?
```

Then:
```
And if you're On Fire, what's the bonus?
```

**If standard mode:**
```
What are your top priorities for today?
```

### 7. Save State

Write today's plan to `.assistant/state.md`:
```markdown
## Today's Plan
date: {today's date}
the_thing: {answer}
would_be_nice: {answer}
on_fire: {answer}

## Current Focus
task: none
status: idle

## Last Check-in
time: never

## Carry Over
<!-- cleared — moved to today's plan -->
```

### 8. Close

```
You're set. Your main focus: {THE Thing}.

Start when you're ready, or say "what should I work on" for a suggestion.
```

---

## ADHD Mode

When `adhd_mode: true` in `.assistant/preferences.md`, enhance the briefing:

- Count today's meetings and calculate context-switching cost (~30-45 min lost per switch). If 3+ meetings, warn about lost hours.
- Identify any 2+ hour meeting-free gaps and label them as "Hyperfocus Windows" in the schedule.
- If morning is clear before 11am, flag it: "Prime deep-work time -- no meetings until X."
- Add a one-line day shape summary, e.g.: "Day shape: Focus morning, meetings afternoon -- front-load deep work."

---

## Notes

- Keep the briefing scannable — bullet points, not paragraphs
- If no calendar, no carry-over, and no tasks, just do weather + planning
- Don't force the user through planning if they seem to want a quick check
- If they say "just give me the briefing" or "skip planning", present info and stop
