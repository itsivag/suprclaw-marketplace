---
name: suprclaw-research
description: Comprehensive web research skill for SuprClaw using web_scrape only, with source-grounded synthesis and explicit citations.
license: Apache-2.0
metadata:
  author: suprclaw
  version: "1.0.0"
---

# SuprClaw Research

Adapted from broad research-skill patterns for SuprClaw runtime constraints.

## Tool Contract

Use `web_scrape` only.

- Do not use browser tools (`cloud_browser_*`, `mobile_browser_*`, relay browser actions) for this skill.
- Research must remain read-only and source-based.

## When To Use

Use this skill for:

- Topic overviews with evidence
- Vendor/tool comparisons
- Market and trend snapshots
- Current-events research with sources
- Decision briefs and recommendation memos

## Research Workflow

1. Define the research objective
- Clarify question, scope, geography, and timeframe.
- Convert broad requests into concrete sub-questions.

2. Gather source candidates
- Use diverse sources (official docs, primary announcements, reputable publications).
- Prefer primary sources for facts, specs, and claims.

3. Extract with `web_scrape`
- Scrape each candidate source.
- Capture publication date and key claims.
- Discard low-signal or duplicative sources.

4. Validate and triangulate
- Cross-check critical claims across multiple sources.
- Mark uncertainty explicitly where evidence conflicts or is missing.

5. Synthesize into decision-ready output
- Provide concise findings, tradeoffs, risks, and recommendation.
- Include explicit source links for each key claim.

## Output Format

Use this structure by default:

1. Objective
2. Key Findings
3. Evidence (source-linked)
4. Tradeoffs / Risks
5. Recommendation
6. Open Questions

## Quality Bar

- No uncited factual claims
- No hallucinated numbers, dates, or quotes
- Date-sensitive claims must include exact dates
- Conflicts between sources must be called out directly
