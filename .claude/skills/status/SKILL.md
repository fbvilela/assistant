---
name: status
description: System health dashboard. Shows profile status, installed skills, folder health, and configured integrations.
---

# Status

Show system health at a glance.

## Data Dependencies
- READS: `.assistant/profile.md`
- READS: `.assistant/preferences.md`
- READS: `.assistant/integrations.md`
- READS: `.claude/skills/` (all installed skills)
- READS: `00-Inbox/`, `01-Projects/`, `02-Areas/`, `03-Resources/`, `04-Archives/`, `Daily Plans/`, `Permanent Notes/`

## Instructions

### 1. Check Profile

Read `.assistant/profile.md`. If it exists, show name and role. If not, flag as not configured.

### 2. Count Skills

List all directories in `.claude/skills/` that contain a `SKILL.md` file. Count them.

### 3. Check Folders

Verify each PARA folder exists and count contents:
- `00-Inbox/Daily/` — count .md files (daily captures)
- `01-Projects/` — count .md files
- `02-Areas/` — count .md files
- `03-Resources/` — count .md files
- `04-Archives/` — count .md files
- `Daily Plans/` — find most recent plan
- `Permanent Notes/` — count .md files
- `Meeting Notes/` — count .md files

### 4. Check Integrations

Read `.assistant/integrations.md`. List what's configured and what's not.

### 5. Present

```
## Assistant Status

**Profile:** {name}, {role} (or "Not configured — run /setup")
**ADHD Mode:** {enabled/disabled}
**Skills installed:** {count}

**PARA Folders:**
  00-Inbox/      {N} daily captures
  01-Projects/   {N} active
  02-Areas/      {N} areas
  03-Resources/  {N} references
  04-Archives/   {N} archived
  Daily Plans/   Last: {date or "none yet"}
  Perm. Notes/   {N} notes
  Meeting Notes/ {N} notes

**Integrations:**
  Calendar       {configured/not configured}
  Email          {configured/not configured}
  Messaging      {configured/not configured}

**Tips:**
{If anything is not configured:}
- Run /setup to configure your profile
- Run /skills to discover integrations
{If inbox has items:}
- You have {N} inbox items — say "process my inbox" to process them
```

---

## Notes

- This is informational. Don't auto-fix anything (that's /heal).
- Keep it scannable — dashboard style, not paragraphs.
- Suggest actionable next steps based on what's missing.
