---
name: draft
description: Draft an email or message. Adapts tone and format based on context.
---

# Draft

Help write an email or message.

## Data Dependencies
- READS: `.assistant/profile.md` (name, for signature)
- READS: `.assistant/preferences.md` (communication_style)

## Instructions

### 1. Gather Context

If the user provided details (e.g., "draft an email to Sarah about the quarterly report"), extract:
- **Recipient**: who is it for?
- **Topic**: what is it about?
- **Tone**: any specific tone requested?

If details are missing, ask one at a time:

```
Who's this for? (name or role, e.g., "a client", "my boss", "John from accounting")
```

Then:
```
What's it about? (brief description)
```

Then:
```
What tone?
1. Professional
2. Friendly
3. Formal
4. Apologetic
```

### 2. Draft

Read `.assistant/profile.md` for the user's name (for signature).
Read `.assistant/preferences.md` for default communication_style if no tone specified.

Generate a draft:

```
Here's a draft:

---
Subject: {subject line}

Hi {recipient},

{body — concise, clear, appropriate tone}

{sign-off},
{user's name}
---

Adjust? (tone / shorter / longer / looks good)
```

### 3. Iterate

If the user wants changes, apply them and show the updated draft.
Don't re-ask all the questions. Just adjust what they asked for.

### 4. Learn (Optional)

If the user consistently changes the sign-off (e.g., always changes "Best regards" to "Cheers"), note it in `.assistant/preferences.md` under `## Learned`:
```
email_sign_off: Cheers
```

---

## Notes

- Keep drafts concise by default. Business emails should be short.
- Don't add filler phrases ("I hope this email finds you well")
- Match the formality to the relationship (client vs. colleague)
- If the user pastes text and says "reply to this", draft a reply to that text
