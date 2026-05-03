---
name: lead-finder
description: Use when the user asks to find potential leads, identify people or companies to contact, extract leads from comments or DMs, build a target list, or find prospects in a niche or audience segment.
metadata:
  version: 1.0.0
---

# Lead Finder

Identify potential leads from available context and turn them into a prioritized prospect list.

## Inputs To Use

Use only provided or accessible context: target audience, niche, comments, DMs, public pages, inbound messages, connected-tool summaries, or user-provided lists. Do not invent identities, contact details, company facts, or buying intent.

## Qualification Signals

Look for:

- Explicit pain or problem mention
- Comment/DM keyword or call raiser signal
- Role or company fit
- Recent trigger event
- Buying intent or urgency
- Existing relationship/warmth
- Clear next conversation path

## Output Format

```markdown
# Lead List

## Summary
- Target segment: ...
- Source reviewed: ...
- Assumptions: ...

## Prioritized Leads
| Priority | Lead | Source | ICP fit | Buying signal | Pain/use case | Confidence | Suggested next step |
|---|---|---|---|---|---|---|---|

## Low Confidence / Research More
| Lead | Why uncertain | Info needed |
|---|---|---|

## Suggested Outreach Angles
1. ...
2. ...
3. ...
```

## Rules

- Separate observed facts from inferred lead quality.
- If contact info is unavailable, say so instead of guessing.
- Do not scrape private channels or bypass platform limits.
- Do not send outreach without explicit approval.
