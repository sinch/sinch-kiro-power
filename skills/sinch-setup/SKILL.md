---
name: sinch-setup
description: "Configures credentials for the Sinch MCP servers bundled with this plugin, and diagnoses why Sinch MCP tools are missing, failing to authenticate, or returning 401/403 errors. Covers the canonical PROJECT_ID, KEY_ID, and KEY_SECRET environment variables, optional Conversation settings, legacy aliases, and how to verify the sinch and sinch-docs servers are connected. Use when Sinch MCP tools are unavailable or unauthenticated, when setting this plugin up for the first time, or when the user asks how to supply Sinch credentials."
license: Apache-2.0
metadata:
  author: Sinch
  version: 1.0.0
  category: Setup
  tags: setup, credentials, mcp, authentication, configuration, troubleshooting
  uses: sinch-authentication
---

# Sinch Plugin Setup

## Overview

This plugin ships two MCP servers, declared in `mcp.json` at the plugin root:

| Server | Transport | Credentials | Purpose |
|---|---|---|---|
| `sinch` | stdio (`npx -y @sinch/mcp`) | **Required** | Call Conversation API tools — send messages, manage webhooks, list senders |
| `sinch-docs` | streamable-http (`https://developers.sinch.com/mcp`) | None | Search and read Sinch developer documentation |

`sinch-docs` works immediately with no configuration. Only `sinch` needs credentials.

## Why there is no `env` block in `mcp.json`

Under the Agent Plugins specification, an MCP server's `env` values are **visible package data**, and
plugins must not embed credentials in them. The specification also expands only two placeholders —
`${PLUGIN_ROOT}` and `${PLUGIN_DATA}` — and only inside `args`, `env` values, and `cwd`.

This matters for a specific failure mode. Writing `"KEY_SECRET": "${KEY_SECRET}"`
does **not** read that variable from the environment. The text is not a recognised placeholder, so it is
passed through **literally**: the server receives the literal string `${KEY_SECRET}`
as the secret and authentication fails with a confusing 401 rather than a clear configuration error.

So this plugin declares `sinch` with no `env` block at all. Credentials come from the environment the
agent client launches the server in. If you are debugging a 401, check the client's environment — not
`mcp.json`.

## Credential contract

Project credentials use the same names across Sinch products and the Build MCP:

| Variable | Value |
|---|---|
| `PROJECT_ID` | Your Sinch project ID |
| `KEY_ID` | Your access key ID |
| `KEY_SECRET` | Your access key secret |

Conversation messaging can also use:

| Variable | Value |
|---|---|
| `CONVERSATION_REGION` | Region of your app — `us`, `eu`, or `br` (defaults to `us`) |
| `CONVERSATION_APP_ID` | The Conversation app ID to operate on |
| `DEFAULT_SMS_ORIGINATOR` | Default sender for SMS workflows |

The old names `CONVERSATION_PROJECT_ID`, `CONVERSATION_KEY_ID`, and
`CONVERSATION_KEY_SECRET` carry the same values. Direct command fallbacks accept them temporarily,
but `@sinch/mcp` reads the canonical names. Do not configure both sets; migrate to the canonical names.

## Getting the credentials

1. Create a Sinch account at [dashboard.sinch.com](https://dashboard.sinch.com/).
2. Open [Conversation API](https://dashboard.sinch.com/convapi/overview), accept the terms, and click
   **Get access**.
3. Create an access key at [Settings → Access keys](https://dashboard.sinch.com/settings/access-keys).
   The secret is shown **once** — capture it immediately.
4. Find your app ID and region on the Conversation API **Apps** page.

For the underlying auth model — OAuth2 token exchange, token lifetime, and region-specific hosts — read
the [sinch-authentication](../sinch-authentication/SKILL.md) skill.

## Agent instructions

When a user asks to set this up, or when Sinch MCP tools fail to authenticate:

1. **Check what is already set** before asking for anything. Report whether the canonical variables are
   present. If one is absent, check its legacy `CONVERSATION_*` alias and report that migration is needed.
   Never print the value of `KEY_SECRET` or `CONVERSATION_KEY_SECRET`, and never echo a secret into a
   file the user has not asked you to write.

   ```bash
   for v in PROJECT_ID KEY_ID KEY_SECRET CONVERSATION_REGION CONVERSATION_APP_ID; do
     if [ -n "${!v}" ]; then echo "$v: set"; else echo "$v: MISSING"; fi
   done
   ```

2. **Ask where the user wants credentials stored.** Do not decide for them — the right answer depends on
   the client and on whether the machine is shared. Offer, as an open question: the agent client's own
   settings file, a shell profile, or a secret manager the user already uses.

3. **Never write credentials into a file inside this plugin.** The plugin directory is package data and
   may be committed, archived, or redistributed. If the user asks you to, say why it is unsafe and offer
   client settings instead.

4. **Restart the MCP server after changing the environment.** The client launches `npx -y @sinch/mcp` as
   a subprocess and it inherits the environment as it existed at launch. Exported variables do not reach
   an already-running server.

## Where each client reads the environment from

Placement is client-specific — the Agent Plugins specification deliberately leaves the base subprocess
environment to the client, which may inherit, omit, or sanitise ambient variables. If the variables are
set in your shell but the server still reports missing credentials, the client is not inheriting the
ambient environment; use its own settings mechanism instead.

- **VS Code** — the environment VS Code itself was launched with, or its MCP configuration.
- **Cursor** — Cursor's MCP settings.
- **Generic / CI** — exported in the process that starts the agent.

## Verifying

Work through these in order; each isolates a different layer.

1. **Plugin loads and is conformant.** The generated Build package should load both MCP servers and its
   generated skills.
2. **Docs server responds.** Ask for anything documentation-shaped — it needs no credentials, so a
   failure here points at network or client MCP config, not at your Sinch account.
3. **Build server authenticates.** List senders. A 401 or 403 means the credentials did not reach the
   subprocess; re-check step 1 of the agent instructions and restart the server.
4. **Region matches.** A valid key with the wrong `CONVERSATION_REGION` fails against a region-specific
   host. Confirm the app's region in the dashboard rather than assuming `us`.

## Troubleshooting

| Symptom | Cause | Fix |
|---|---|---|
| No Sinch tools at all | Client did not load `mcp.json`, or does not support MCP | Confirm the client implements the Agent Plugins MCP component; check its logs |
| Only `sinch-docs` tools appear | `sinch` failed to start | Check `npx` is on PATH and `@sinch/mcp` can be fetched |
| 401 / 403 on every call | Canonical credentials absent, legacy aliases only, or literal `${...}` text reaching the server | Verify `PROJECT_ID`, `KEY_ID`, and `KEY_SECRET` in the client's environment; never place `${VAR}` in `mcp.json` |
| Auth works, calls 404 | Wrong `CONVERSATION_APP_ID` or region | Re-read both from the dashboard |
| Skills missing after install | Incomplete package | Reinstall the complete generated package |
