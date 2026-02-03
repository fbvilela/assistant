---
name: find-skills
description: Search for and install agent skills from the open skills ecosystem. Use when the user wants to find, browse, or install new skills and capabilities.
aliases:
  - sk
argument-hint: "<search query>"
---

# Find & Install Skills

Search the open agent skills ecosystem and install new capabilities.

Examples:
- `/find-skills outlook email`
- `/sk project management`
- "is there a skill for WhatsApp?"

## Instructions

### 0. Check Recommended Skills First

Before searching the ecosystem, read `.assistant/recommended-skills.md`. This file contains curated, vetted skills matched to common needs. Check if the user's query matches any trigger phrases listed there.

If a match is found, present the recommended skill first with its description, install command, setup requirements, and URL. Then offer to also search the broader ecosystem if they want alternatives.

### 1. Search the Ecosystem

If no match in recommended-skills.md, or the user wants more options:

Use the query provided as $ARGUMENTS. If no arguments given, ask what kind of skill they're looking for.

```bash
npx skills find "$ARGUMENTS" 2>/dev/null
```

### 2. Present Results

For each result, show:
- Skill name and a brief description of what it likely does
- Install command
- Link to learn more on skills.sh

Example:
```
Found some options:

1. canifi-life-os@outlook — Outlook email management via browser automation
   Install: npx skills add andrejones92/canifi-life-os@outlook
   More: https://skills.sh/andrejones92/canifi-life-os/outlook

2. email-composer — Template-based email drafting
   Install: npx skills add davila7/claude-code-templates@email-composer
   More: https://skills.sh/davila7/claude-code-templates/email-composer

Want me to install any of these?
```

If no results:
```
No skills found for "{query}". Try different keywords, or I can help
with this directly.

You can also browse all skills at: https://skills.sh/
```

### 3. Install if Requested

If the user wants to install:
```bash
npx skills add <owner/repo@skill> -g -y
```

After installing:
- Update `.assistant/integrations.md` if the skill adds a new integration
- Let the user know they need to restart the session for the skill to become available

### 4. Other Commands

If the user asks about updates or checking skills:
- `npx skills check` — Check for updates
- `npx skills update` — Update all installed skills
- Browse at: https://skills.sh/

---

## Notes

- This is how the assistant grows. Users discover capabilities over time.
- If a user describes a need that matches a known skill, proactively suggest it
- Always show the skills.sh link so users can read more before installing
