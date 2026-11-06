# Pamba MCP examples

Connect an MCP client (Claude Code, Codex, Cursor or any client that speaks Streamable HTTP) to [Pamba](https://pamba.app), which makes AI-avatar videos and slideshows and schedules them to TikTok and Instagram.

- **Endpoint:** `https://api.pamba.app/mcp` (Streamable HTTP)
- **Auth:** a workspace API key in the `X-API-Key` header (workspace switcher → Settings → API keys), or OAuth from a chat app that supports remote MCP
- **Surface:** about 400 tools in 9 toolsets
- **Docs:** [MCP server guide](https://pamba.app/help/mcp-server) · [tool reference](https://pamba.app/help/mcp-tool-reference) · [overview](https://pamba.app/developers/mcp-server) · [REST API](https://pamba.app/api)

## Connect

Claude Code:

```sh
claude mcp add --transport http pamba https://api.pamba.app/mcp --header "X-API-Key: <your workspace API key>"
```

Codex (`~/.codex/config.toml`, or the project's `.codex/config.toml`):

```toml
[mcp_servers.pamba]
url = "https://api.pamba.app/mcp"
http_headers = { "X-API-Key" = "<your workspace API key>" }
```

Any client that takes a JSON server list:

```json
{
  "mcpServers": {
    "pamba": {
      "type": "http",
      "url": "https://api.pamba.app/mcp",
      "headers": { "X-API-Key": "<your workspace API key>" }
    }
  }
}
```

Keep the key out of chat messages and out of version control.

## Start safely

Three switches on the endpoint URL shape a connection:

| Switch | What it does |
|---|---|
| `?readonly=true` | Loads only read-only tools. A write tool is unknown to the connection, so it cannot be talked into one. |
| `?toolsets=videos,avatars` | Loads only the named toolsets: `videos`, `editing`, `avatars`, `accounts`, `ideas`, `discover`, `content`, `automation`, `workspace`. |
| `?max_credits=500` | Refuses any single credit-spending call whose up-front estimate is above 500 credits, and charges nothing for it. |

They combine: `https://api.pamba.app/mcp?toolsets=accounts,videos&readonly=true`.

## Things to know before you automate

- **Posts are real.** Scheduled posts go out in public from real TikTok and Instagram accounts and stay up. Review every video before it is scheduled.
- **Generation spends credits.** Video generation and replication spend the workspace's credits. Use `max_credits` on autonomous clients.
- **Work outlives the connection.** Scheduled posts still publish, and campaigns keep spending, after you disconnect, until you turn them off in Pamba.
- **AI labels are opt-in.** `ai_label: true` on `schedule_post` turns on TikTok's AI-generated content label and Instagram's AI label before posting. Label realistic AI content: both platforms require it.

## Examples

Prompts to try, each in [`examples/`](examples/). Start with a read-only connection.

1. [List what is in the workspace](examples/01-list-avatars.md) (read-only)
2. [Read last month's analytics](examples/02-analytics.md) (read-only)
3. [Make a video and schedule it](examples/03-make-and-schedule.md) (spends credits, posts publicly)

## License

MIT. See [LICENSE](LICENSE).
