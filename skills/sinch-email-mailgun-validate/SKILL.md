---
name: sinch-email-mailgun-validate
description: "Validate an email address via Mailgun Validate API"
license: Apache-2.0
user-invocable: true
disable-model-invocation: true
metadata:
  author: Sinch
  version: "1.0.0"
  category: Command
  generated-from: src/commands/email/mailgun/validate.md
---
# Validate Email Address (Mailgun)

Validate a single email address or run bulk validation using the Mailgun Validate API. Returns deliverability, risk, disposable/role detection. Uses Basic Auth (api:API_KEY).

**IMPORTANT: Execute this command directly. Do NOT generate script files. Perform the API call immediately.**

## Input

- `--address` / `-a`: Email address to validate - required
- `--format` / `-f`: Output format (table or json) - optional

Arguments: whatever the user typed after the command name, which may be nothing.

## Instructions

**Execute these steps directly - do not write code or scripts:**

0. If the request has no details: ask for email address to validate. Otherwise parse.

1. Validate: --address (valid email format). Get MAILGUN_API_KEY. Base: api.mailgun.net or api.eu.mailgun.net per MAILGUN_REGION. If missing, report "Mailgun is not configured. Set MAILGUN_API_KEY."

2. GET https://api.mailgun.net/v4/address/validate?address={email} (or api.eu.mailgun.net for EU) with Basic Auth (api:API_KEY).

3. Display result: deliverable/undeliverable, risk, is_disposable_address, is_role_address, reason, did_you_mean. "✅ Validation complete". Handle 401, 400.

4. Handle all errors gracefully.

## Examples

```
/sinch:email:mailgun:validate --address=user@example.com
/sinch:email:mailgun:validate -a test@example.com --format=json
```

## API Reference

- **Endpoint**: GET /v4/address/validate?address={email}
- **Auth**: Basic api:API_KEY
