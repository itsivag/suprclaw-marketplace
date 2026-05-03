---
name: reply-summarizer
description: Use when the user asks to summarize customer replies, lead responses, email threads, DMs, sales call notes, objections, or inbound messages into intent, pain, objections, and next actions.
metadata:
  version: 1.0.0
---

# Reply Summarizer

Turn customer replies into sales intelligence and next actions.

## Extract

- Lead identity/source
- Intent level
- Pain or desired outcome
- Objections
- Buying stage
- Decision-maker or stakeholder hints
- Urgency/timeline
- Required follow-up
- Suggested response

## Output Format

```markdown
# Customer Reply Summary

## Overall Read
- ...

## Reply Breakdown
| Lead | Intent | Pain/use case | Objection | Stage | Next action | Suggested reply |
|---|---|---|---|---|---|---|

## Patterns
- ...

## Risks / Unclear Items
| Item | Why unclear | Clarifying question |
|---|---|---|
```

## Rules

- Quote or paraphrase the source signal behind each conclusion.
- Do not infer budget, authority, or urgency unless supported.
- Separate objections from simple questions.
