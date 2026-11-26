---
name: sinch-email-mailgun-optimize
description: "Check email deliverability and domain health via Mailgun Optimize (InboxReady)"
license: Apache-2.0
user-invocable: true
disable-model-invocation: true
metadata:
  author: Sinch
  version: "1.0.0"
  category: Command
  generated-from: src/commands/email/mailgun/optimize.md
---
# Mailgun Optimize (InboxReady)

Check email deliverability, blocklist status, and domain health using Mailgun Optimize (InboxReady). List monitored domains, check reputation, test inbox placement. Uses Basic Auth (api:API_KEY).

**IMPORTANT: Execute this command directly. Do NOT generate script files. Perform the API call immediately.**

## Input

- `--action` / `-a`: Action: list-domains, check-blocklist, health - optional, default list-domains
- `--domain` / `-d`: Domain to check (for blocklist/health) - optional
- `--format` / `-f`: Output format (table or json) - optional

Arguments: whatever the user typed after the command name, which may be nothing.

## Instructions

**Execute these steps directly - do not write code or scripts:**

0. If the request has no details: ask what to do (list monitored domains, check blocklist, check domain health). Otherwise parse.

1. Validate: --action, optional --domain. Get MAILGUN_API_KEY. Base: api.mailgun.net. If missing, report "Mailgun is not configured."

2. GET https://api.mailgun.net/v1/inboxready/domains (or relevant Optimize endpoint per action) with Basic Auth (api:API_KEY). For domain-specific checks use appropriate endpoint and --domain.

3. Display: list of domains, blocklist status, or health summary. "✅ Optimize results". Handle 401, 404.

4. Handle all errors gracefully.

## Examples

```
/sinch:email:mailgun:optimize
/sinch:email:mailgun:optimize --action=list-domains
/sinch:email:mailgun:optimize --action=check-blocklist --domain=mydomain.com
```

## API Reference

- **Endpoint**: GET /v1/inboxready/domains and other InboxReady endpoints
- **Auth**: Basic api:API_KEY
