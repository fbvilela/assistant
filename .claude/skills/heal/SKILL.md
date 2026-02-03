---
name: heal
description: Diagnose and fix broken skills, missing files, or corrupted configuration. Self-repair for the assistant.
---

# Heal

Diagnose and fix issues with the assistant.

## Data Dependencies
- READS: `.assistant/profile.md`
- READS: `.assistant/preferences.md`
- READS: `.assistant/integrations.md`
- READS: `.assistant/state.md`
- READS: `.claude/skills/*/SKILL.md` (all skills)
- READS: All key folders
- WRITES: Any file that needs repair

## Instructions

### 1. Check .assistant/ Data Store

Verify each file exists and has content:

- `.assistant/profile.md` — must have `name:` field at minimum
- `.assistant/preferences.md` — must have `adhd_mode:` and `communication_style:` fields
- `.assistant/integrations.md` — must exist
- `.assistant/state.md` — must exist

Report status for each. If missing, flag it.

### 2. Check CLAUDE.md

Read `CLAUDE.md` and verify it has:
- Data Files table
- Command Routing section
- Available Commands table

If corrupted or missing critical sections, offer to restore.

### 3. Validate Skills

List all directories in `.claude/skills/`. For each, check:
- `SKILL.md` file exists
- File is non-empty
- Has YAML frontmatter (starts with `---`)
- Has `name:` and `description:` in frontmatter

Expected core skills (21):
setup, good-morning, plan, whats-next, end-of-day, checkin,
capture, tasks, inbox, done, stuck, draft, polish,
plan-week, week, help, find-skills, status, update, heal, profile

Report missing or broken skills.

### 4. Check Folders

Verify existence of PARA folders:
- `00-Inbox/` (with `Daily/` and `Fleeting-Notes/` subdirectories)
- `01-Projects/`
- `02-Areas/`
- `03-Resources/`
- `04-Archives/`
- `Daily Plans/`
- `Permanent Notes/`
- `Meeting Notes/`

### 5. Report

```
Running diagnostics...

.assistant/ Data Store
  profile.md        {ok/MISSING/INVALID}
  preferences.md    {ok/MISSING/INVALID}
  integrations.md   {ok/MISSING}
  state.md          {ok/MISSING}

CLAUDE.md           {ok/CORRUPTED}

Skills ({N} of 21 expected)
  {skill}  ok    {skill}  ok    {skill}  MISSING
  ...

Folders
  00-Inbox/      {ok/MISSING}
  01-Projects/   {ok/MISSING}
  02-Areas/      {ok/MISSING}
  03-Resources/  {ok/MISSING}
  04-Archives/   {ok/MISSING}
  Daily Plans/   {ok/MISSING}
  Perm. Notes/   {ok/MISSING}
  Meeting Notes/ {ok/MISSING}

{N} issues found.
```

### 6. Fix

If issues found, ask:
```
Want me to fix these? (y/n)
```

Fixes:
- **Missing .assistant/ files** → re-run /setup
- **Missing PARA folders** → create them (00-Inbox, 01-Projects, 02-Areas, 03-Resources, 04-Archives, Daily Plans, Permanent Notes, Meeting Notes)
- **Missing skills** → attempt to re-download or recreate from template
- **Corrupted CLAUDE.md** → offer to restore from known-good version
- **Invalid YAML in skills** → show the error and offer to fix

After fixing:
```
Fixed {N} issues. Run /status to verify.
```

---

## Notes

- Always ask before fixing. Never auto-repair.
- If profile.md is missing, the best fix is to re-run /setup
- For missing skills, try `npx skills add` first; if that fails, warn the user
- Keep the diagnostic output clean and scannable
