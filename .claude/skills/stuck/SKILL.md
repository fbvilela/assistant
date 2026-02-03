---
name: stuck
description: Help when overwhelmed or unable to start. Breaks tasks into tiny steps. ADHD-friendly overwhelm handler.
---

# Stuck / Overwhelmed

When a task feels too big, break it down.

## Data Dependencies
- READS: `.assistant/state.md` (current focus, today's plan)
- READS: `.assistant/preferences.md` (adhd_mode)
- WRITES: `.assistant/state.md` (updated focus with first step)

## Instructions

### 1. Identify What's Stuck

If the user says what's bothering them, use that.

If not, read `.assistant/state.md` for current focus or THE Thing:
```
Is it "{THE Thing from state.md}" that feels too big?
Or something else?
```

### 2. Diagnose (Briefly)

Don't label the user. Just adapt the approach:

**Can't start (initiation block):**
→ Focus on the smallest first step

**Too many things (cognitive overload):**
→ Pick just one. Hide the rest.

**Don't know how (unclear path):**
→ Help clarify the outcome, then work backwards

**Feels pointless or boring (motivation):**
→ Pair with something enjoyable, or find a smaller win first

### 3. Break It Down

Ask:
```
What does "done" look like for this? Not perfect — just done enough.
```

Then break into steps of 10-15 minutes each:
```
Here's how I'd break this down:

1. {tiny concrete step} (~10 min)
2. {next step} (~15 min)
3. {next step} (~10 min)

You don't have to do all of these. Just #1. Ready?
```

**Rules for steps:**
- Each step must be a concrete physical action (not "think about" but "open the document and write the first paragraph")
- Maximum 10-15 minutes each
- Maximum 5 steps shown (even if there are more)
- First step should be trivially easy

### 4. The 2-Minute Start

If ADHD mode, offer the 2-minute technique:
```
Try this: commit to just 2 minutes on step 1.
Set a timer. When it goes off, you can stop guilt-free.

Most of the time, you'll keep going. But if not, that's 2 minutes
of progress you didn't have before.
```

### 5. Update State

If the user picks a step, update `.assistant/state.md`:
```markdown
## Current Focus
task: {step 1 description}
started: {current time}
status: in-progress
```

---

## ADHD Mode

When `adhd_mode: true` in `.assistant/preferences.md`, enhance task breakdown:

- Break tasks into sub-1-hour micro-tasks with clear success criteria for each.
- Make the first step trivially easy -- under 5 minutes, zero ambiguity.
- Include dopamine feedback for each chunk: what does "done" look like? What can you check off or see working?
- Auto-decompose: if a task has no clear first step, generate a 3-step decomposition before asking the user to start.

---

## Notes

- NEVER say "just do it" or "just start"
- NEVER guilt-trip about procrastination
- The goal is to make the first step so small it feels effortless
- "What would done enough look like?" is the most powerful question
- If they're truly overwhelmed across everything (not just one task), suggest: "Let's pick just ONE thing. Everything else can wait."
- Acknowledge that being stuck is normal, not a character flaw
