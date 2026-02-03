---
name: update
description: Check for and apply skill updates from the skills ecosystem.
aliases:
  - up
---

# Update Skills

Check for newer versions of installed skills and update them.

## Instructions

### 1. Check for Updates

```bash
npx skills check 2>/dev/null
```

### 2. Present Results

If updates available:
```
Skill updates available:

  {skill-name}    {current} → {new version}
  {skill-name}    {current} → {new version}
  {skill-name}    up to date

Update all? (y/n)
```

If no updates:
```
All skills are up to date.
```

If the command fails:
```
Couldn't check for updates. Make sure you have an internet connection
and Node.js installed.
```

### 3. Apply Updates

If the user confirms:
```bash
npx skills update 2>/dev/null
```

After updating, let the user know:
```
Skills updated. Restart your session (exit and run `claude` again)
for changes to take effect.
```

### 4. Verify

After updating, run a quick check that skill files still exist:
- List `.claude/skills/*/SKILL.md`
- If any are missing, warn and suggest `/heal`

---

## Notes

- Always show what's changing before applying
- Don't auto-update without confirmation
- If updates break something, /heal can fix it
