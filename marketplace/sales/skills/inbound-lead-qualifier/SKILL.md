---
name: inbound-lead-qualifier
description: Use when the user asks to qualify inbound leads, score prospects, determine who is worth responding to first, or evaluate customer fit from replies, forms, comments, DMs, or emails.
metadata:
  version: 1.0.0
---

# Inbound Lead Qualifier

Qualify inbound leads by fit, signal strength, and next action.

## Scoring Model

Score each lead using:

- ICP fit: role, company, market, use case
- Pain clarity: specific problem vs vague interest
- Urgency: active timeline or trigger
- Authority: decision-maker, influencer, unknown
- Budget/proxy: budget mentioned, company size, paid tool usage, unknown
- Engagement: reply quality, questions asked, requested demo, keyword/comment signal
- Next-step clarity: obvious reply, call, demo, or nurture path

## Output Format

```markdown
# Inbound Lead Qualification

| Rank | Lead | Fit | Intent | Pain | Authority | Budget/proxy | Urgency | Score | Recommended next step |
|---|---|---|---|---|---|---|---|---|---|

## Best Leads To Prioritize
1. ...
2. ...
3. ...

## Nurture / Not Ready
| Lead | Reason | Suggested nurture reply |
|---|---|---|

## Missing Info To Qualify
| Lead | Missing info | Question to ask |
|---|---|---|
```

## Rules

- Do not over-score polite interest as buying intent.
- Mark unknown fields as `Unknown`, not negative.
- Recommend the smallest next step that advances qualification.
