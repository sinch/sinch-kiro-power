---
name: sinch-help
description: "Show overview of all Sinch commands and product guides available in this plugin"
license: Apache-2.0
user-invocable: true
disable-model-invocation: true
metadata:
  author: Sinch
  version: "1.0.0"
  category: Command
  generated-from: src/commands/help.md
---
# Sinch Command and Guide Overview

Display a concise overview of all Sinch commands and product guides available in this plugin. Do NOT generate script files. Output the overview directly.

## Instructions

**Display the following structure directly - do not write code or scripts:**

1. **Messaging (Conversation API)**
   - /sinch:api:messages:send — Send text (SMS/RCS)
   - /sinch:api:messages:send-media — Send media (image, video, document)
   - /sinch:api:messages:send-card — Send RCS rich card
   - /sinch:api:messages:send-carousel — Send RCS carousel
   - /sinch:api:messages:send-choice — Send choice/buttons
   - /sinch:api:messages:send-location — Send location
   - /sinch:api:messages:list — List messages
   - /sinch:api:senders:list — List active numbers (Numbers API)

2. **Webhooks**
   - /sinch:api:webhooks:create, list, update, delete, triggers

3. **Batch & Templates**
   - /sinch:api:batch:send — Send batch (up to 1000 recipients)
   - /sinch:api:batch:status — Batch job status
   - /sinch:api:templates:list, create, delete

4. **Voice & Verification**
   - /sinch:api:voice:callout — TTS outbound call
   - /sinch:api:voice:calls — Call info
   - /sinch:api:verification:start — Start phone verification (SMS/Flashcall/Call)
   - /sinch:api:verification:check — Report verification code

5. **Fax & Numbers**
   - /sinch:api:fax:send, list
   - /sinch:api:numbers:lookup — Number lookup (carrier, etc.)
   - /sinch:api:numbers:search — Search available numbers to rent

6. **Email**
   - /sinch:email:mailgun:send, validate, inspect, optimize

7. **Infrastructure & Admin**
   - /sinch:api:10dlc:brands, campaigns
   - /sinch:api:sip:trunks
   - /sinch:api:provisioning:setup — WhatsApp/RCS senders
   - /sinch:api:contacts:list

8. **Product guides (full skill catalogue)**
   - Messaging: sinch-conversation-api (omnichannel messaging); sinch-sms (SMS sender IDs, encoding, opt-out behaviour); sinch-mms (MMS media in the US, Canada, and Australia); sinch-rcs (rich cards, carousels, SMS fallback); sinch-whatsapp (WhatsApp Business and template messages)
   - Voice and verification: sinch-voice-api (Voice API v1, TTS, IVR, conferencing, SVAML); sinch-voice-api-v2 (Voice API v2 public preview, SVAML v2, Voice Relay); sinch-in-app-calling (in-app voice/video SDKs); sinch-elastic-sip-trunking (SIP trunks and PSTN routing); sinch-verification-api (SMS, flashcall, call, data, and WhatsApp verification)
   - Numbers and provisioning: sinch-numbers-api (search, rent, manage, release); sinch-number-order-api (KYC number orders); sinch-number-lookup-api (carrier, line type, SIM swap checks); sinch-porting-api (port-in orders and activation); sinch-imported-numbers-hosting-orders (import and text-enable non-Sinch numbers); sinch-10dlc (US 10DLC registration); sinch-provisioning-api (WhatsApp, RCS, and KakaoTalk senders and templates)
   - Fax: sinch-fax-api (send/receive faxes, fax-to-email, cover pages)
   - Email: sinch-mailgun (send, receive, track); sinch-mailgun-validate (verification and list hygiene); sinch-mailgun-inspect (pre-send quality and accessibility); sinch-mailgun-optimize (inbox placement and deliverability)
   - Functions and CLI: sinch-functions (Functions beta platform); sinch-functions-node (Node.js/TypeScript runtime); sinch-functions-dotnet (C#/.NET runtime); sinch-cli (`sinch` terminal commands)
   - SDKs and authentication: sinch-sdks (Node.js, Python, Java, and .NET client initialisation); sinch-authentication (OAuth2, Basic auth, application signing, API keys)

9. **Config & Help**
   - /sinch:config:auth — Authentication setup guide
   - /sinch:help — This overview

**Tip**: Run any command with no arguments for interactive mode. Use the authentication command or your agent client's settings to check configured credentials.
