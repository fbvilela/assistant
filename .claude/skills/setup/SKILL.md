---
name: setup
description: First-run setup wizard. Personalizes the assistant by asking about the user and creating configuration files. Re-run anytime to change settings.
---

# Setup Wizard

Personalize the assistant for a new user, or re-configure an existing setup.

## Data Dependencies
- WRITES: `.assistant/profile.md`
- WRITES: `.assistant/preferences.md`
- WRITES: `.assistant/integrations.md`
- WRITES: `.assistant/state.md`
- CREATES: Folders and task files if missing

## Instructions

### 1. Detect First Run vs Re-run

Check if `.assistant/profile.md` exists.

**First run:**
```
Welcome! I'm your personal assistant. Let me learn a bit about you
so I can be actually useful.

Before we start — this assistant organizes your tasks, notes, and
projects as markdown files using the GTD (Getting Things Done) method.
To browse and edit those files visually, install Obsidian:

  https://obsidian.md

It's free and runs on Mac, Windows, and Linux. Once installed, open
this folder as a vault. You can do this later — the assistant works
without it, but Obsidian makes everything much nicer to browse.

This setup takes about 2 minutes.
```

**Re-run:**
Read existing `.assistant/profile.md` and show current values.
```
Let's update your settings. I'll show your current values — just press
Enter to keep them, or type a new value.
```

### 2. Ask Questions (One at a Time)

Ask each question individually. Wait for the answer before asking the next one. Do NOT present all questions at once.

**Q1 - Name:**
"What should I call you?"

**Q2 - Role:**
"What do you do? (e.g., business manager, developer, freelancer, student)"

**Q3 - Company (optional):**
"Do you work for a company? If so, which one? (or skip)"

**Q4 - Tools:**
"What tools or apps do you use daily for work? (e.g., Outlook, Gmail, Slack, Google Calendar, Notion)"
- Store the raw answer. This helps suggest integrations later.

**Q5 - ADHD Mode:**
"Would you like ADHD-friendly features? These include gentler reminders, shorter task lists, a 'stuck' helper, and no shame-based motivation. (yes/no)"

**Q6 - Communication Style:**
"How should I communicate with you?"
- Direct and brief
- Friendly and conversational
- Professional and formal

**Q7 - Location:**
"Where are you based? (city or region, for weather and timezone)"
- Infer timezone from location. If ambiguous, ask.

**Q8 - Work Hours:**
"When do you usually work? (e.g., 9-5, 8-6, flexible, varies)"

### 3. Create .assistant/ Files

#### `.assistant/profile.md`
```markdown
name: {answer to Q1}
role: {answer to Q2}
company: {answer to Q3, or "none"}
location: {answer to Q7}
timezone: {inferred timezone, e.g., Australia/Melbourne}
work_hours: {answer to Q8}
weather_location: {city from Q7}
tools: {comma-separated from Q4}
```

#### `.assistant/preferences.md`
```markdown
adhd_mode: {true/false from Q5}
communication_style: {direct/friendly/professional from Q6}
task_structure: {if ADHD: "3-things", else: "standard"}
time_estimate_multiplier: {if ADHD: "3x", else: "1.5x"}
checkin_interval: {if ADHD: "2h", else: "none"}
transition_buffer: {if ADHD: "15min", else: "5min"}
max_options: {if ADHD: "3", else: "5"}

## Learned
<!-- The assistant adds patterns it notices over time -->
```

#### `.assistant/integrations.md`

Detect available integrations based on the tools answer (Q4) and what's installed on the system.

Check for `icalBuddy`:
```bash
which icalBuddy 2>/dev/null
```

```markdown
## Calendar
type: {apple-calendar if icalBuddy found, else "none"}
tool: {icalBuddy path if found, else "none"}
status: {configured if found, else "not-configured"}

## Email
type: none
status: not-configured

## Messaging
type: none
status: not-configured

## Notes
- Tools the user mentioned: {from Q4}
- Run /find-skills to discover integrations for these tools
```

#### `.assistant/state.md`
```markdown
## Today's Plan
date: {today's date}
the_thing: not set
would_be_nice: not set
on_fire: not set

## Current Focus
task: none
status: idle

## Last Check-in
time: never

## Carry Over
<!-- Items from yesterday's end-of-day -->
```

### 4. Configure Second Brain

The second-brain skill needs to know the vault path. Since the vault IS this project folder, write the config automatically — no need to ask the user.

```bash
mkdir -p ~/.second-brain
```

Write `~/.second-brain/config.json`:
```json
{
  "vaultPath": "{absolute path to this project folder}",
  "setupComplete": true,
  "userName": "{answer to Q1}",
  "userContext": "Permanent Notes/Assisting-User-Context.md",
  "preferences": {
    "defaultCaptureType": "inbox",
    "proactiveCapture": true,
    "inboxThreshold": 5
  }
}
```

Get the absolute path by running `pwd` in the project root.

### 5. Create PARA Folders if Missing

Check and create if they don't exist:
- `00-Inbox/` with `Daily/` and `Fleeting-Notes/` subdirectories
- `01-Projects/`
- `02-Areas/`
- `03-Resources/` with `Reference-Notes/` subdirectory
- `04-Archives/`
- `Daily Plans/`
- `Permanent Notes/`
- `Meeting Notes/`

Only create folders that are missing. Don't overwrite existing content.

### 6. Show Summary

```
All set, {name}! Here's what I can do:

DAILY WORKFLOW
  /gm          Good morning — start your day
  /plan        Plan or replan your day
  /next        What should I do next?
  /eod         End of day — wrap up
  {if ADHD:}
  /checkin     Check in on your progress
  /stuck       Help when you're overwhelmed

CAPTURE & TASKS
  /c <text>    Quick capture a thought
  /tasks       Show today's tasks
  /inbox       Process captured items
  /done        Mark something complete

COMMUNICATION
  /draft       Draft an email or message
  /polish      Improve a draft

WEEKLY
  /pw          Plan the week
  /week        Review the past week

SYSTEM
  /help        Show this list anytime
  /skills      Find and install new skills
  /profile     Change your settings
  /status      System health check

Or just talk to me naturally — I understand plain language too.

{If tools were mentioned that aren't integrated yet:}
Tip: You mentioned using {tools}. Run /find-skills to see if there are
integrations available for those.
```

---

## Notes

- Keep the wizard conversational, not form-like
- One question at a time is critical — especially for ADHD users
- If re-running, show current values and let user skip unchanged fields
- Don't be verbose in confirmations. The summary at the end is enough.
