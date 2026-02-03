---
name: week
description: Review the past week's activity. What got done, what carried over, patterns noticed.
aliases:
  - w
---

# Week Review

Summarize the past week.

## Data Dependencies
- READS: `Daily Plans/` (last 7 days of daily plans)
- READS: `Daily Plans/Week-of-*.md` (weekly plan if exists)
- READS: `.assistant/preferences.md` (adhd_mode)

## Instructions

### 1. Gather Data

Read daily plans from the last 7 days: `Daily Plans/{YYYY-MM-DD}.md` for each day from today-7 to today-1.

Read `Daily Plans/Week-of-*.md` for the most recent weekly plan priorities.

### 2. Compile Summary

```
## Week in Review ({date range})

**Planned priorities:**
- {priority 1} — {done/not done}
- {priority 2} — {done/not done}
- {priority 3} — {done/not done}

**Completed this week:**
- {all items from daily notes "Done" sections}

**Carried over repeatedly:**
- {items that appear in multiple days' "Carried Over" sections}

**Days with daily plans:** {X of 7}
```

### 3. Patterns (if enough data)

If there are 3+ daily plans:
```
**Patterns I noticed:**
- {e.g., "You completed more tasks on mornings with no meetings"}
- {e.g., "Task X has carried over 3 days — might need breaking down"}
```

### 4. Close

If ADHD mode:
```
You got {priorities done} of {priorities planned} priorities done. That's real progress.

{If something carried over multiple days:}
"{task}" has been carrying over. Want me to break it down? (/stuck)
```

If standard:
```
{X} tasks completed across {Y} days. {Z} priorities achieved.

Ready to plan next week? (/plan-week)
```

---

## Notes

- This is reflective and encouraging, not evaluative
- If few daily plans exist, don't guilt — just note "3 of 7 days tracked"
- Highlighting repeated carry-overs is useful, not judgmental
- Suggest /plan-week at the end to flow into next week's planning
