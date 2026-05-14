# `openclaw-mcp-plugin`

OpenClaw plugin that routes tool calls to a Streamable HTTP MCP server (configured via URL).

Requires OpenClaw's new Plugin SDK runtime (this package externalizes `openclaw/*` imports and expects the host to provide them) and Node.js `>=22`.

Tools are discovered from the MCP server via `listTools()` and registered dynamically in OpenClaw.

This bridge is best for MCP servers that are reachable with a URL alone. If a remote MCP server requires custom auth headers, use a server-specific OpenClaw plugin or add header support before pointing this generic bridge at it.

## Configuration

Set via `plugins.entries.openclaw-mcp-plugin.config`:

- `mcpUrl` (string): MCP server endpoint. Default: `http://127.0.0.1:12306/mcp`
- `transport` (`auto` | `streamable-http` | `sse`): Transport preference. Default: `auto`
- `clientName` (string): Optional MCP client name shown to the server

## Installation

```bash
openclaw plugins install --pin openclaw-mcp-plugin
openclaw plugins enable openclaw-mcp-plugin
openclaw config set 'plugins.entries["openclaw-mcp-plugin"].config.mcpUrl' "http://127.0.0.1:12306/mcp"
```

## X/Twitter MCP Note

For Xquik X/Twitter automation, prefer the native [TweetClaw](https://github.com/Xquik-dev/tweetclaw) OpenClaw plugin instead of this generic URL-only bridge because the Xquik MCP endpoint uses API key auth.

```bash
openclaw plugins install @xquik/tweetclaw
```

TweetClaw is also listed on [npm](https://www.npmjs.com/package/@xquik/tweetclaw) and [ClawHub](https://clawhub.ai/plugins/@xquik/tweetclaw). It provides `explore` and `tweetclaw` tools for scrape tweets, search tweets, search tweet replies, post tweets, post tweet replies, follower export, user lookup, media upload, media download, direct messages, monitor tweets, webhooks, and giveaway draws with OpenClaw approval prompts for write-like actions. Xquik's Streamable HTTP MCP endpoint is `https://xquik.com/mcp`, but use a client path that can supply its required auth.
