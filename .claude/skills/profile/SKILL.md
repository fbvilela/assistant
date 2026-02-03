---
name: profile
description: View or edit your profile and preferences. Quick targeted changes without re-running the full setup wizard.
---

# Profile

View or change settings.

## Data Dependencies
- READS: `.assistant/profile.md`
- READS: `.assistant/preferences.md`
- READS: `.assistant/integrations.md`
- WRITES: `.assistant/profile.md` (if changes made)
- WRITES: `.assistant/preferences.md` (if changes made)

## Instructions

### 1. If No Arguments — Show Profile

Read all three files and present:

```
## Your Profile

**Name:** {name}
**Role:** {role}
**Company:** {company}
**Location:** {location} ({timezone})
**Work Hours:** {work_hours}

**Preferences:**
- ADHD Mode: {enabled/disabled}
- Communication Style: {style}
- Check-in Interval: {interval}
- Time Estimate Buffer: {multiplier}

**Integrations:**
- Calendar: {status}
- Email: {status}
- Messaging: {status}

**Learned Preferences:**
{contents of ## Learned section from preferences.md, if any}

Change anything? Just tell me what to update.
Or run /setup to redo the full wizard.
```

### 2. If Arguments — Apply Change

If the user says something like:
- "change my name to Alex" → update profile.md `name:` field
- "turn off ADHD mode" → update preferences.md `adhd_mode: false`
- "change location to Sydney" → update profile.md `location:`, `timezone:`, `weather_location:`
- "make me professional style" → update preferences.md `communication_style: professional`

Read the relevant file, make the change, write it back.

Confirm:
```
Updated: {field} → {new value}
```

### 3. Learned Preferences

If the user asks about learned preferences:
```
These are patterns I've noticed over time:
- {preference}: {value}

Want me to remove any of these?
```

---

## Notes

- Quick and targeted. Don't walk through the whole wizard for one change.
- Infer timezone from location changes.
- If the user changes ADHD mode, mention what it affects: "ADHD mode disabled. Check-ins and the /stuck command are still available, but the gentler tone and 3-things structure will switch to standard mode."
