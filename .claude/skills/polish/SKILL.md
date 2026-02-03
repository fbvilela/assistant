---
name: polish
description: Improve existing text — emails, messages, documents. Makes it clearer, more concise, or adjusts tone.
---

# Polish

Improve a piece of text.

## Data Dependencies
- READS: `.assistant/preferences.md` (communication_style)

## Instructions

### 1. Get the Text

If the user pasted text, use it directly.

If not:
```
Paste the text you'd like me to improve.
```

### 2. Ask What to Improve (Optional)

If the user specified (e.g., "make this more professional" or "shorten this"), do that.

If not, apply sensible defaults:
- Tighten language (remove filler words)
- Fix grammar and punctuation
- Improve clarity
- Maintain the original voice and intent

### 3. Present

Show the improved version with a brief note on what changed:

```
Here's the polished version:

---
{improved text}
---

Changes: tightened wording, fixed 2 grammar issues, clearer call-to-action.

Good to go, or want me to adjust further?
```

### 4. Iterate

If the user wants more changes, apply them. Don't re-explain what you did — just show the new version.

---

## Notes

- Preserve the user's voice. Don't make everything sound like ChatGPT.
- Don't add content they didn't write. Polish means refine, not expand.
- For emails: remove "I hope this finds you well" and similar filler
- Quick and practical. Don't over-explain the changes.
