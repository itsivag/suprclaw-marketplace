---
name: suprclaw-cloud-browser
description: Required cloud browser workflow for interactive browsing, takeover, and session lifecycle in SuprClaw.
license: Apache-2.0
metadata:
  author: suprclaw
  version: "1.0.0"
---

# SuprClaw Cloud Browser

Use only the SuprClaw cloud browser tools for interactive browsing.

Workflow:
- Start with `cloud_browser_open`.
- Use `cloud_browser_exec` for navigation and interactions.
- Use `cloud_browser_request_takeover` for MFA, CAPTCHA, payments, or destructive actions.
- Resume with `cloud_browser_resume` after takeover.
- Close with `cloud_browser_close` once the task is complete.

Prefer search or scrape tools for read-only tasks. Use browser automation only when interaction or authenticated state is required.
