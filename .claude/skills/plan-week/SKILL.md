---
name: plan-week
description: Interactive weekly planning session. Review what's ahead and set priorities for the week.
aliases:
  - pw
---

# Plan Week

Set priorities for the week ahead.

## Data Dependencies
- READS: `.assistant/profile.md` (name)
- READS: `.assistant/preferences.md` (adhd_mode)
- READS: `.assistant/integrations.md` (calendar)
- READS: `01-Projects/` (active projects with next actions)
- READS: `02-Areas/` (area tasks and responsibilities)
- READS: `Daily Plans/` (recent daily plans for carry-over)
- WRITES: `Daily Plans/Week-of-YYYY-MM-DD.md` (weekly plan)

## Instructions

### 1. Gather Context

**Calendar (if configured):**
```bash
icalBuddy -f -n -ea -nc -ps "| : |" -po "title,datetime" eventsFrom:today to:today+7d 2>/dev/null
```

**Active projects:**
List files in `01-Projects/` — read each for status and next actions.

**Areas of responsibility:**
Scan `02-Areas/` for any High Priority or Next Actions items.

**Someday/Maybe items:**
Check `01-Projects/` and `02-Areas/` for items in Someday/Maybe sections that could be pulled into this week.

**Last week's carryover:**
Read recent `Daily Plans/` files for anything still open.

### 2. Present Overview

```
## This Week

**Calendar highlights:**
- Monday: Team standup, Client call
- Wednesday: Review meeting
- Friday: (clear)

**Open from last week:**
- {carried over tasks from recent daily plans}

**Active projects (01-Projects/):**
- {project}: next action is {X}
- {project}: next action is {Y}

**Area tasks (02-Areas/):**
- {area}: {high priority or next action items}

**Someday/Maybe candidates:**
- {items from Someday/Maybe sections that could be done this week}
```

### 3. Set Priorities

If ADHD mode:
```
Pick up to 3 things that MUST happen this week.
Everything else is bonus. What are your 3?
```

If standard:
```
What are your priorities for this week?
```

### 4. Write Weekly Plan

Create `Daily Plans/Week-of-YYYY-MM-DD.md`:

```markdown
# Week of {date range}

## Priority
- [ ] {priority 1}
- [ ] {priority 2}
- [ ] {priority 3}

## Should Do
- [ ] {task}

## If Time Permits
- [ ] {task}
```

### 5. Close

```
Week planned. Your 3 priorities:
1. {priority 1}
2. {priority 2}
3. {priority 3}

Start tomorrow with /gm to break these into daily tasks.
```

---

## ADHD Mode

When `adhd_mode: true` in `.assistant/preferences.md`, adjust weekly planning:

- Budget max 2 deliberate project switches per day. If more are needed, batch similar work together.
- Protect Mon/Wed/Fri mornings as deep-work blocks. Suggest batching meetings and reviews to Tue/Thu afternoons.
- If any priority item is vague or multi-day, break it into sub-1-hour chunks with clear success criteria.
- If user picks 5+ priorities, push back: "That's a lot of context switches. Can we group any of these?"

---

## Notes

- Weekly planning should feel strategic, not overwhelming
- ADHD mode: cap at 3 priorities. More than that and nothing gets done.
- Pull from backlog actively — items rot there if you don't surface them
- If a project has no next action, flag it: "This project needs a next step"
