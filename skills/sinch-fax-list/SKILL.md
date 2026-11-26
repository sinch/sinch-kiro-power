---
name: sinch-fax-list
description: "List faxes (sent/received) via Sinch Fax API"
license: Apache-2.0
user-invocable: true
disable-model-invocation: true
metadata:
  author: Sinch
  version: "1.0.0"
  category: Command
  generated-from: src/commands/api/fax/list.md
---
# List Faxes

List faxes for your project using the Sinch Fax API. Supports pagination. Uses OAuth2.

**IMPORTANT: Execute this command directly. Do NOT generate script files. Perform the API call immediately.**

## Input

- `--format` / `-f`: Output format (table or json) - optional, default table
- `--page-size` / `-n`: Number of results - optional

Arguments: whatever the user typed after the command name, which may be nothing.

## Instructions

**Execute these steps directly - do not write code or scripts:**

0. If the request has no details: use defaults (table format). Otherwise parse.

1. Get CONVERSATION_* or FAX_* env vars. GET https://fax.api.sinch.com/v3/projects/{projectId}/faxes with OAuth2. If missing, report "Sinch API is not configured."

2. Format response: table (id, to, status, createdAt, etc.) or JSON. Display "✅ Faxes listed" with count.

3. Handle 401, 404. Handle all errors gracefully.

## Examples

```
/sinch:api:fax:list
/sinch:api:fax:list --format=json
```

## API Reference

- **Endpoint**: GET /v3/projects/{projectId}/faxes
- **Documentation**: https://developers.sinch.com/docs/fax/
