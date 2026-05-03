---
name: meeting-summary
description: Use when the user asks to summarize a meeting, call, transcript, notes, standup, planning session, retrospective, or discussion and extract decisions, action items, risks, and follow-ups.
metadata:
  version: 1.0.0
---

# Meeting Summary

Turn meeting notes or transcripts into a concise, actionable record.

## Extract

- Meeting topic, date, and participants when present
- Key discussion points
- Decisions and rationale
- Action items with owner and due date
- Risks, blockers, dependencies
- Open questions
- Follow-ups and next meeting needs

## Output Format

```markdown
# Meeting Summary - [Topic]

## Context
- Date: TBC
- Participants: TBC
- Source: notes/transcript/context provided

## Summary
- ...

## Decisions
| Decision | Rationale | Owner | Impact |
|---|---|---|---|

## Action Items
| Priority | Action | Owner | Due | Acceptance criteria |
|---|---|---|---|---|

## Risks / Blockers
| Risk | Impact | Owner | Mitigation |
|---|---|---|---|

## Open Questions
| Question | Owner | Needed by |
|---|---|---|

## Follow-Ups
| Follow-up | With | Timing | Draft |
|---|---|---|---|
```

## Rules

- Mark missing participants, dates, owners, or due dates as `TBC`.
- Do not include verbatim transcript unless requested.
- Keep decisions separate from discussion.
- Do not send meeting notes or create external tasks without approval.
