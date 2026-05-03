---
name: comment-dm-converter
description: Use when the user asks to turn comments, DMs, replies, social engagement, or keyword comments like TEAM into sales conversations and draft replies.
metadata:
  version: 1.0.0
---

# Comment DM Converter

Turn social engagement into respectful sales conversations.

## Process

1. Identify the commenter/DM sender and their signal.
2. Classify the signal: interest, pain, curiosity, objection, request, support, low intent.
3. Draft a reply that continues the conversation naturally.
4. Avoid jumping directly to a hard sell unless the signal is explicit.
5. Suggest the next step only if earned by the context.

## Output Format

```markdown
# Comment / DM Replies

| Person | Signal | Intent | Recommended reply | Next step |
|---|---|---|---|---|

## Batch Reply Templates
### High intent
...

### Curious but vague
...

### Objection or concern
...

### Keyword/comment trigger
...
```

## Rules

- Do not pretend the user has read private profile data unless provided.
- Do not spam identical replies; vary based on signal.
- Keep replies human, brief, and non-pushy.
- Do not send replies without explicit approval.
