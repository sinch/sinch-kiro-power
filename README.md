# Sinch Agent Plugin

Build communication experiences with Sinch from your agent. Explore official documentation, get implementation guidance, and — where live tools are available — work with Sinch services without leaving your development workflow.

Use the plugin across messaging, voice, verification, numbers, fax, and email:

- Build messaging experiences with SMS, MMS, RCS, WhatsApp, templates, rich content, and channel fallback.
- Create and manage webhooks, senders, and messaging applications.
- Verify users, place voice calls, and send or receive faxes.
- Search, rent, look up, port, and provision phone numbers.
- Register US 10DLC brands and campaigns, and configure SIP trunking.
- Send and validate email with Mailgun, and review email quality and deliverability.
- Find product documentation, authentication guidance, SDK examples, and implementation patterns.

Some marketplace listings provide documentation and guidance only. Listings with live tools enabled can also perform supported API actions after credentials are configured.

## Prerequisites

- A supported agent client.
- A [Sinch account](https://dashboard.sinch.com/?utm_source=agent_plugin&utm_medium=marketplace&utm_campaign=sinch_agent_plugin) for live API actions. Documentation and implementation guidance do not require one.

## Installation

Find **Sinch** in your agent's plugin marketplace and select **Install** or **Add**. The marketplace handles the plugin package and updates.

If you are reviewing a local package, point the client's plugin installer at the package root.

## Setup

Documentation search works as soon as the plugin is installed. No credentials are required.

For live Conversation API and Numbers tools, configure:

| Variable | Where to find it |
|---|---|
| `PROJECT_ID` | The project selector in the [Sinch dashboard](https://dashboard.sinch.com/dashboard?utm_source=agent_plugin&utm_medium=marketplace&utm_campaign=sinch_agent_plugin) |
| `KEY_ID` | [Settings → Access keys](https://dashboard.sinch.com/settings/access-keys?utm_source=agent_plugin&utm_medium=marketplace&utm_campaign=sinch_agent_plugin) |
| `KEY_SECRET` | Shown once when an access key is created |
| `CONVERSATION_APP_ID` | [Conversation API → Apps](https://dashboard.sinch.com/convapi/apps?utm_source=agent_plugin&utm_medium=marketplace&utm_campaign=sinch_agent_plugin) |
| `CONVERSATION_REGION` | Your app region: `us`, `eu`, or `br` (defaults to `us`) |

Only the first three are needed for all live tools. A messaging workflow may also need the app ID, region, and `DEFAULT_SMS_ORIGINATOR`.

Other services use their own credentials:

- **Voice and Verification:** `APPLICATION_KEY` and `APPLICATION_SECRET`, available from the application's page in the dashboard.
- **Mailgun:** `MAILGUN_API_KEY`, plus `MAILGUN_DOMAIN` and `MAILGUN_SENDER_ADDRESS` when sending email.

Set credentials in the environment or secret settings used by your agent client, then restart the client or its MCP server. Never add secrets to the plugin files or commit them to source control.

Ask the agent to help configure Sinch if tools are missing or return 401/403 errors.

## Usage

Ask in ordinary language. For example:

```
Show me how to send an RCS message with SMS fallback.
Send an SMS to +15551234567 saying the delivery is on its way.
Create a webhook for message delivery and inbound message events.
Verify +15551234567 with an SMS one-time password.
Find available phone numbers in the United States.
Make a text-to-speech call to +15551234567.
Send an email with Mailgun from notifications@mycompany.com to ada@example.com.
Validate the email address ada@example.com.
```

When commands are available in your listing, `/sinch-help` shows the installed workflows.

## Common workflows

| Area | Example workflows |
|---|---|
| Messaging | Send text, media, cards, carousels, choices, and locations; use templates and channel fallback |
| Webhooks and templates | Create, list, update, and delete webhooks; manage message templates |
| Voice and verification | Place calls, inspect calls, start verification, and check a verification code |
| Numbers and provisioning | Search and look up numbers, list senders, and provision channels |
| Compliance and connectivity | Manage 10DLC brands and campaigns, and configure SIP trunks |
| Email | Send with Mailgun; validate, inspect, and run Mailgun Optimize |
| Documentation | Search official Sinch docs and follow product-specific implementation guides |

## MCP servers

The plugin can expose two Sinch MCP servers:

| Server | Purpose | Credentials |
|---|---|---|
| **Sinch Docs** (`sinch-docs`) | Search and read official Sinch developer documentation | None |
| **Sinch Build** (`sinch`) | Use supported Sinch APIs and operational tools | Required for the service being used |

Feature availability depends on the marketplace listing. A documentation-only listing provides Sinch Docs and product guidance without live API actions.

## Help and troubleshooting

- Ask the agent to configure Sinch or diagnose missing tools.
- If documentation works but live tools do not, confirm the required credentials are visible to the agent client and restart its MCP server.
- A 401 or 403 usually means credentials are missing, invalid, or not available to the process that started the live tools.
- Confirm that the Conversation app and its region match.

## Links

- [Sinch Developer Documentation](https://developers.sinch.com/?utm_source=agent_plugin&utm_medium=marketplace&utm_campaign=sinch_agent_plugin)
- [Sinch Dashboard](https://dashboard.sinch.com/?utm_source=agent_plugin&utm_medium=marketplace&utm_campaign=sinch_agent_plugin)
- [Sinch Help Centre](https://sinch.com/help-center/?utm_source=agent_plugin&utm_medium=marketplace&utm_campaign=sinch_agent_plugin)

## Telemetry

Where supported and enabled by the tool it runs in, this integration may collect limited telemetry to help Sinch understand usage and improve the experience. This telemetry does not include personal data, message content, or the content of your files.

Telemetry follows the controls provided by the tool the integration is running in. Where the tool provides telemetry or data-sharing settings, you can manage the applicable preference through those settings.

## Privacy

Your use of Sinch services through this integration is subject to the [Sinch Privacy Notice](https://sinch.com/legal/privacy-notice/?utm_source=agent_plugin&utm_medium=marketplace&utm_campaign=sinch_agent_plugin) and, where applicable, the [Sinch Data Processing Agreement](https://sinch.com/legal/terms-and-conditions/other-sinch-terms-conditions/data-processing-agreement/?utm_source=agent_plugin&utm_medium=marketplace&utm_campaign=sinch_agent_plugin).

Credentials you provide are stored by the tool this integration runs in, using that tool's own credential or settings storage. Sinch does not receive or store your credentials outside of authenticated API calls you initiate.

## Use of Sinch Services

This integration provides developers with a way to interact with Sinch APIs and services from supported developer tools and environments. Use of Sinch services requires a valid Sinch account and is subject to the applicable [Sinch Terms of Service](https://sinch.com/legal/terms-and-conditions/other-sinch-terms-conditions/terms-of-service/?utm_source=agent_plugin&utm_medium=marketplace&utm_campaign=sinch_agent_plugin) and [Acceptable Use Policy](https://sinch.com/legal/policies-statements/sinch-voice-policies-statements/acceptable-use-policy/?utm_source=agent_plugin&utm_medium=marketplace&utm_campaign=sinch_agent_plugin).

This integration may be used in conjunction with third-party developer tools, IDEs, platforms, registries, or environments that are not operated or controlled by Sinch. Such third-party tools and platforms are subject to their own terms and policies.

This integration is provided on an "as-is" basis. Sinch is not responsible for the operation, availability, performance, or security of any third-party tool or platform.

## Important

This integration is a developer tool that helps you work with Sinch APIs from within a supported environment. It is not a standalone service and does not itself provide communications services. Sinch APIs accessed through it require a Sinch account, and your use of those APIs is subject to the applicable terms governing your use of Sinch services.

## Licence

Apache-2.0

Copyright Sinch AB, [https://sinch.com](https://sinch.com/?utm_source=agent_plugin&utm_medium=marketplace&utm_campaign=sinch_agent_plugin)

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at:

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.

## Feedback, Issues and Support

We welcome feedback, and we are here to help if you run into any issues.

- For questions about Sinch APIs or your Sinch account, visit the [Sinch Help Centre](https://sinch.com/help-center/?utm_source=agent_plugin&utm_medium=marketplace&utm_campaign=sinch_agent_plugin).
- For issues with this integration, [contact Sinch Support](https://support.sinch.com/?utm_source=agent_plugin&utm_medium=marketplace&utm_campaign=sinch_agent_plugin).

We will continue to enhance this integration with new features in future.

From all of us at Sinch, happy coding!
