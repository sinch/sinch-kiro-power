---
name: sinch-verification-check
description: "Report verification code to complete phone verification (Sinch Verification API)"
license: Apache-2.0
user-invocable: true
disable-model-invocation: true
metadata:
  author: Sinch
  version: "1.0.0"
  category: Command
  generated-from: src/commands/api/verification/check.md
---
# Check / Report Verification Code

Report the verification code entered by the user to complete a Sinch Verification. Uses the verification ID returned from the start command. Uses Application Key + Secret.

**IMPORTANT: Execute this command directly. Do NOT generate script files. Perform the API call immediately.**

## Input

- `--id` / `-i`: Verification ID (from start command) - required
- `--code` / `-c`: Code entered by the user (e.g. PIN from SMS) - required
- `--method` / `-m`: Method used (sms, flashcall, callout) - optional, default sms

Arguments: whatever the user typed after the command name, which may be nothing.

## Instructions

**Execute these steps directly - do not write code or scripts:**

0. If the request has no details: ask for verification ID and the code the user entered. Otherwise parse.

1. Validate: --id (non-empty), --code (non-empty), optional --method (default sms).

2. Get Verification API application key and secret from env. If missing, report "Verification API is not configured."

3. Request body: method ("sms" or as specified), sms: { code: "<code>" } (for SMS method). Use appropriate body for flashcall/callout if API differs.

4. PUT https://verification.api.sinch.com/verification/v1/verifications/id/{verificationId} with Basic Auth, body with method and code.

5. On success: "✅ Verification successful" or "Verification completed". On invalid code: "❌ Invalid or expired code." Handle 404, 401, 400 with clear messages.

6. Handle all errors gracefully.

## Examples

```
/sinch:api:verification:check --id=VERIFICATION_ID --code=1234
/sinch:api:verification:check -i VERIFICATION_ID -c 5678 --method=sms
```

## API Reference

- **Endpoint**: PUT /verification/v1/verifications/id/{verificationId}
- **Auth**: Basic (application_key:application_secret)
- **Documentation**: https://developers.sinch.com/docs/verification/
