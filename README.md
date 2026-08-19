# Sinch Kiro Power for AWS Kiro

A [Kiro Power](https://kiro.dev) that connects the [Sinch Build platform](https://dashboard.sinch.com?utm_source=aws_kiro&utm_medium=extension_listing) to your AI-assisted development workflow — send SMS, WhatsApp, and RCS messages, verify phone numbers, make voice calls, and manage virtual numbers without leaving your IDE.

## Install

1. Open Kiro
2. Go to **Powers** → **Install from GitHub**
3. Enter: `github.com/sinch/sinch-kiro-power`

## Setup

Export credentials to your shell profile (`~/.zshrc` or `~/.bash_profile`):

```bash
# Required
echo 'export PROJECT_ID=your_project_id' >> ~/.zshrc
echo 'export KEY_ID=your_key_id' >> ~/.zshrc
echo 'export KEY_SECRET=your_key_secret' >> ~/.zshrc
source ~/.zshrc
```

Find your credentials in the [Sinch Dashboard](https://dashboard.sinch.com?utm_source=aws_kiro&utm_medium=extension_listing):
- `PROJECT_ID` — shown in the top toolbar
- `KEY_ID` / `KEY_SECRET` — under Settings → Access Keys

Restart Kiro after setting variables.

## What you can do

| Say this in Kiro | What happens |
|------------------|-------------|
| "Send an SMS with Sinch" | Guides you through sending a message with confirmation |
| "Send a WhatsApp message using a template" | Lists your templates and sends with approval |
| "Verify a phone number with OTP" | Sends an OTP and submits the code |
| "Make a text-to-speech voice call" | Places a TTS call with confirmation |
| "Find available phone numbers in the US" | Searches and rents virtual numbers |

## Workflows

- **[Get Started](steering/get-started.md)** — validate credentials, send first message
- **[Conversation & Templates](steering/messaging-campaigns.md)** — WhatsApp templates, multi-channel, interactive messages
- **[Voice, Verification & Numbers](steering/voice-verification-numbers.md)** — OTP, TTS calls, virtual number management

## License

[Apache-2.0](LICENSE)
