---
name: sinch-templates-list
description: "List message templates from Sinch Template Management API (V2)"
license: Apache-2.0
user-invocable: true
disable-model-invocation: true
metadata:
  author: Sinch
  version: "1.0.0"
  category: Command
  generated-from: src/commands/api/templates/list.md
---
# List Message Templates

List all omni-channel message templates for your project using the Sinch Template Management API V2. Templates can have multiple translations and variables.

**IMPORTANT: Execute this command directly. Do NOT generate script files. Perform the API call immediately.**

## Input

- `--format` / `-f`: Output format (table or json) - optional, default table

Arguments: whatever the user typed after the command name, which may be nothing.

## Instructions

**Execute these steps directly - do not write code or scripts:**

0. If the request has no details: use default format (table). Otherwise parse --format.

1. Validate: --format (table|json). Get CONVERSATION_* env vars. Template API base: https://{region}.template.api.sinch.com (us, eu, br). If missing, report "Sinch API is not configured."

2. GET https://{region}.template.api.sinch.com/v2/projects/{projectId}/templates with OAuth2 Bearer token.

3. Format response: table (id, description, default_translation, version, translation count) or raw JSON. Display "✅ Templates listed" with count.

4. Handle errors (401, 404) with clear messages. Handle all errors gracefully.

## Examples

```
/sinch:api:templates:list
/sinch:api:templates:list --format=json
```

## API Reference

- **Base URL**: https://{region}.template.api.sinch.com (V2 only; V1 end-of-life)
- **Endpoint**: GET /v2/projects/{project_id}/templates
- **Documentation**: https://developers.sinch.com/docs/conversation/templates/
