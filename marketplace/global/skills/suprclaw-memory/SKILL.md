---
name: suprclaw-memory
description: Persistent memory tool for storing and retrieving user context across conversations.
license: Apache-2.0
metadata:
  author: suprclaw
  version: "1.0.0"
---

# SuprClaw Memory

You have access to persistent memory that survives across all conversations with this user.
Use it proactively when it improves continuity.

## When to store memory
- User preferences (communication style, tools, workflows, tech stack)
- Decisions made during tasks (chosen approach, rejected alternatives)
- Important facts about the user's projects, goals, or constraints

## When to retrieve memory
- At the start of a new conversation: call `memory_search` by topic or `memory_get_all` for full context
- Before making recommendations: check if there are relevant past preferences
- When the user references something from a past session

## Tool reference
- `memory_add` — store new facts
- `memory_search` — semantic search over stored memories
- `memory_get_all` — retrieve all stored memories
- `memory_delete` — remove a specific memory by id
- `memory_delete_all` — wipe all memories only when explicitly requested

## Rules
- Never expose raw memory ids to the user.
- Do not store sensitive credentials or secrets.
- Keep memories concise.
