# Adside MCP Server

Official documentation and client configuration for the [Adside](https://www.adside.ai) MCP server —
AI agents that manage paid ads on **Meta, LinkedIn, and Google Ads**, operable from any MCP client.

- **Registry:** [`ai.adside/adside`](https://registry.modelcontextprotocol.io/v0/servers?search=ai.adside) on the official MCP Registry
- **Endpoint:** `https://api.adside.ai/mcp` (streamable HTTP, JSON-RPC 2.0, stateless)
- **Auth:** `Authorization: Bearer sk_live_…` — API key from your Adside account
- **Docs:** https://docs.adside.ai/mcp-protocol

## Quick start

### Claude Code
```bash
claude mcp add --transport http adside https://api.adside.ai/mcp \
  --header "Authorization: Bearer sk_live_YOUR_KEY"
```

### Any MCP client (JSON config)
```json
{
  "mcpServers": {
    "adside": {
      "type": "streamable-http",
      "url": "https://api.adside.ai/mcp",
      "headers": { "Authorization": "Bearer sk_live_YOUR_KEY" }
    }
  }
}
```

### Raw JSON-RPC
```bash
curl -X POST https://api.adside.ai/mcp \
  -H "Authorization: Bearer sk_live_YOUR_KEY" \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":"1","method":"tools/list"}'
```

## What you can do

Adside's agents handle the operational side of paid advertising. Through MCP you can:

- Research competitor and market ad creative
- List and manage campaigns (e.g. `list_meta_campaigns`)
- Build, organize, and bulk-import ad creative
- Run day-to-day campaign operations across Meta, LinkedIn, and Google Ads

Per-channel routes are available (`/{source}/mcp` for `meta`, `linkedin`, `googleads`) — see the
[protocol docs](https://docs.adside.ai/mcp-protocol).

## About

Adside is a team of AI agents that manage your paid advertising — built for performance agencies
and in-house teams. This repository hosts public docs and examples for the hosted MCP server; the
server itself is part of the Adside platform.

Website: https://www.adside.ai · Docs: https://docs.adside.ai · Contact: rob@adside.ai
