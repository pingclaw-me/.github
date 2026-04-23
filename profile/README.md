<p align="center">
  <img src="icon.png" width="96" height="96" alt="PingClaw">
</p>

# PingClaw

**Location context for any AI agent.** One binary, no dependencies.

---

## What it does

PingClaw runs on your phone and gives your AI agent your current location — accurate, current, scoped to you. No history, no map, no notifications.

```
Your phone  →  PingClaw server  →  Your agent (MCP / OpenClaw / webhook)
```

Nothing is stored permanently. Only the single most recent position exists, in memory, with a 24-hour expiry. No database writes, no history, no trails.

---

## Self-hosting

```bash
go install github.com/pingclaw-me/pingclaw-server/cmd/pingclaw-server@latest
pingclaw-server --local
```

That's it. SQLite, in-memory cache, no Redis, no Postgres, no OAuth credentials. The server prints a pairing token — enter it in the app and location starts flowing. Nothing phones home.

The apps have a **Self-Hosted Server** option on the sign-in screen. Enter your server URL and token — no Apple or Google account needed.

For details, see [pingclaw-server](https://github.com/pingclaw-me/pingclaw-server).

---

## Repos

| Repo | What it is |
|---|---|
| [pingclaw-server](https://github.com/pingclaw-me/pingclaw-server) | Go server. `--local` for self-hosting (SQLite), hosted mode for multi-user (Postgres + Redis). Built-in MCP server, OpenClaw push, webhooks. |
| [pingclaw-ios](https://github.com/pingclaw-me/pingclaw-ios) | iOS app (SwiftUI). Background location, Sign in with Apple + Google, self-hosted token pairing. |
| [pingclaw-android](https://github.com/pingclaw-me/pingclaw-android) | Android app (Kotlin, Jetpack Compose). Foreground service, same features. |
| [openclaw-skill](https://github.com/pingclaw-me/openclaw-skill) | OpenClaw skill — teaches the agent to fetch your location on demand. |
| [pingclaw-tools](https://github.com/pingclaw-me/pingclaw-tools) | Development and testing tools: E2E test suites, webhook listener. |

---

## Agent integration

**MCP** — the server includes a built-in MCP server at `/pingclaw/mcp`. Paste-ready config for Claude Code, Claude Desktop, VS Code, Cursor, and Zed. No plugin, no sidecar.

**OpenClaw gateway push** — the server pushes each location update directly to your gateway's `/hooks/` endpoint. Your agent gets your position as context automatically.

**OpenClaw skill** — install the [PingClaw skill](https://github.com/pingclaw-me/openclaw-skill) to let your agent fetch your location on demand via `web_fetch`.

**Webhook** — for other setups, the server POSTs location updates to any URL with a verifiable `Authorization: Bearer` header.

---

## Privacy

- Location held in ephemeral memory only — never written to a database
- 24-hour TTL, overwritten on each update, then gone
- No location history, no movement tracking, no telemetry
- API keys stored as irreversible hashes
- Self-host means you are the only operator — nothing phones home
- All stored data viewable and deletable at any time

---

## MIT

All repos. Do whatever you want with it.

---

Built by [@christianreimer](https://github.com/christianreimer)
