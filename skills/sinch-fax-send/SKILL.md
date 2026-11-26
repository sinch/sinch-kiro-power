---
name: sinch-fax-send
description: "Send a fax via Sinch Fax API"
license: Apache-2.0
user-invocable: true
disable-model-invocation: true
metadata:
  author: Sinch
  version: "1.0.0"
  category: Command
  generated-from: src/commands/api/fax/send.md
---
# Send Fax

Send a fax to a recipient using the Sinch Fax API. Document must be available at a public URL (PDF or other supported format). Uses OAuth2 (project key id/secret).

**IMPORTANT: Execute this command directly. Do NOT generate script files. Perform the API call immediately.**

## Input

- `--to` / `-t`: Recipient fax number (E.164 or national format) - required
- `--content-url` / `-u`: Public URL of the document to fax (e.g. PDF) - required
- `--callback-url` / `-c`: Optional webhook URL for status callbacks

Arguments: whatever the user typed after the command name, which may be nothing.

## Instructions

**Execute these steps directly - do not write code or scripts:**

0. If the request has no details: ask for recipient fax number and document URL. Otherwise parse.

1. Validate: --to (non-empty), --content-url (valid HTTPS URL). Get PROJECT_ID, KEY_ID, KEY_SECRET (or the legacy CONVERSATION_* / FAX_* aliases). Fax API uses OAuth2. Base: https://fax.api.sinch.com/v3. If missing, report "Sinch API is not configured."

2. Request body: to, contentUrl; optional callbackUrl. POST https://fax.api.sinch.com/v3/projects/{projectId}/faxes with OAuth2 Bearer token.

3. On success: "✅ Fax sent" with fax ID. Handle 400, 401, 404 with clear messages.

4. Handle all errors gracefully.

## Examples

```
/sinch:api:fax:send --to=+14155551234 --content-url=https://example.com/document.pdf
/sinch:api:fax:send -t +14155551234 -u https://example.com/doc.pdf
```

## API Reference

- **Base URL**: https://fax.api.sinch.com/v3
- **Endpoint**: POST /projects/{projectId}/faxes
- **Documentation**: https://developers.sinch.com/docs/fax/
