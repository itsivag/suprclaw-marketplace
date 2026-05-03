---
name: response-tracker
description: Use when the user asks who needs a response, what leads are waiting, what sales threads are stale, or how to track follow-ups and open sales loops.
metadata:
  version: 1.0.0
---

# Response Tracker

Identify sales conversations that need attention and organize the response queue.

## Signals

Look for:

- Unanswered customer questions
- Leads waiting on promised material
- Stalled warm conversations
- Demos/calls needing recap or next step
- Objections that need response
- High-intent replies with no clear owner

## Output Format

```markdown
# Sales Response Queue

## Respond First
| Priority | Lead | Waiting on | Since | Why it matters | Draft next response |
|---|---|---|---|---|---|

## Follow Up Later
| Lead | Last touch | Suggested timing | Next step |
|---|---|---|---|

## No Response Needed
| Lead/thread | Reason |
|---|---|

## Unclear / Needs Review
| Thread | Why unclear | What to check |
|---|---|---|
```

## Rules

- Do not mark anything done externally.
- Do not assume a thread is stale without timing or context.
- Draft responses only; sending requires approval.
