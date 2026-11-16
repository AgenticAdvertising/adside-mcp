# Adside MCP server

Connect an AI assistant to your ad accounts. [Adside](https://www.adside.ai) runs a remote MCP server: add its URL to Claude, ChatGPT, Claude Code, Codex or any other MCP client, sign in, and your assistant can read and change campaigns on Meta, Google Ads, LinkedIn, TikTok, Snapchat, Reddit and X, and set up tracking in Google Tag Manager.

```text
https://api.adside.ai/mcp
```

- **Transport:** Streamable HTTP. There is no standalone event stream.
- **Sign-in:** OAuth 2.1 in your browser, with PKCE and dynamic client registration. Where there is no browser, a personal API key.
- **Registry:** [`ai.adside/adside`](https://registry.modelcontextprotocol.io/v0/servers?search=ai.adside) on the official MCP Registry.
- **Docs:** [docs.adside.ai/mcp/connect](https://docs.adside.ai/mcp/connect). Every docs page is also markdown: add `.md` to its URL.

You need an Adside account with at least one workspace. To read or change campaigns on a platform, connect that platform to the workspace in Adside first.

This repository holds the registry entry and the client configuration. The server itself is part of the Adside platform.

## Connect

**Claude Code**

```bash
claude mcp add --transport http adside https://api.adside.ai/mcp
```

Then type `/mcp` and sign in once.

**Codex**

```bash
codex mcp add adside --url https://api.adside.ai/mcp
```

**Claude and ChatGPT**

Add the URL as a custom connector and sign in. The steps for each, with screenshots, are in the [docs](https://docs.adside.ai/mcp/connect).

**Any other MCP client**

```json
{
  "mcpServers": {
    "adside": {
      "type": "http",
      "url": "https://api.adside.ai/mcp"
    }
  }
}
```

## Without a browser

In CI, a scheduled script or a cloud agent, send a personal API key in place of the sign-in. Create one in Adside, under Settings, then API keys. A key can be read only.

```bash
claude mcp add --transport http adside https://api.adside.ai/mcp \
  --header "Authorization: Bearer $ADSIDE_API_KEY"
```

Keys look like `adside_pat_` followed by 49 letters and digits. The setup for Codex, the Claude API, the OpenAI Responses API and n8n is in [Sign-in and API keys](https://docs.adside.ai/authentication).

## What your assistant can do

| Area | Ask it to |
| --- | --- |
| Ad platforms | Read accounts, campaigns, ads, audiences and performance, and create or change them, on every platform the workspace has connected |
| Reporting | Compare spend and CPA across platforms, rank creatives, keep saved reports |
| Creatives | Brief, generate, edit and review creatives in your brand |
| Launching | Upload ads in bulk |
| Research | Track competitors, search ad libraries, save ads to boards |
| Brain | Search and write what Adside knows about a workspace |
| Routines | Schedule recurring work, such as a Monday report |
| Ad comments | Read, reply to and hide comments |

Three tools reach every connected ad platform, so your assistant does not load hundreds of tools it may not need: `search_channel_tools`, `describe_channel_tool` and `call_channel_tool`. The full list is in [What the Adside MCP server can do](https://docs.adside.ai/mcp/capabilities).

A client that loads few tools can ask for some areas only: `https://api.adside.ai/mcp?features=reporting,brain`.

## Before a change

Your assistant acts as you, with your role in Adside. A change that reaches people or is hard to undo takes two calls. The first changes nothing: Adside answers with a plain-language summary and a confirmation token. The second call, with the same input and the token, makes the change. Your assistant reads you the summary and asks before the second call. Every change to an ad platform works this way. See [Confirmations](https://docs.adside.ai/confirmations).

An agent that runs with nobody watching answers its own confirmations. Give it a read-only API key unless its job is to make changes.

## Also

- **The `adside` CLI** reads your ad accounts, generates images and video, and writes reports from a terminal: `npm install -g adside`. See [Install the adside CLI](https://docs.adside.ai/cli/install).
- **The plugin for Claude Code and Codex** sets up the CLI skills and this server together: [AgenticAdvertising/adside-plugin](https://github.com/AgenticAdvertising/adside-plugin).
- **For an AI agent deciding whether to use Adside**, one page: [adside.ai/agents.md](https://www.adside.ai/agents.md).

## Pricing

$290 per brand, per month, with $100 of creative credits included, for as many people and agents as you like. There is a 7-day free trial. See [pricing](https://www.adside.ai/pricing).

Questions: [support@adside.ai](mailto:support@adside.ai)
