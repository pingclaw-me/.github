# PingClaw

**Location context for AI.** A quiet utility, not an app you stare at.

---

## What it does

PingClaw runs on your phone and gives your AI agent a single coordinate when it needs one — accurate, current, scoped to you. No history, no map, no notifications.

If you use [OpenClaw](https://openclaw.ai), [NanoClaw](https://nanoclaw.ai), or any MCP-compatible agent setup, PingClaw is how your agent knows you're at the farmers market and not your desk — without you having to say so.

The data flow:

Your phone  →  PingClaw Server  →  Your agent (OpenClaw webhook / MCP)


What gets transmitted:

[27.1396° S · 109.4270° W](https://www.google.com/maps?q=-27.1396,-109.4270)  ±8m  source: gps

Nothing is stored permanently. The server holds your most recent position in memory for up to 24 hours, overwrites it on the next update, and that's it. No database, no history, no trails. You can inspect every record stored about your account or delete it entirely at [pingclaw.me](https://pingclaw.me).

---

## The three repos

| Repo | What it is |
|---|---|
| [pingclaw-server](https://github.com/pingclaw-me/pingclaw-server) | Go server. Receives location from the apps, caches it in Redis, delivers to your agent via webhook or MCP. |
| [pingclaw-ios](https://github.com/pingclaw-me/pingclaw-ios) | Swift / SwiftUI. Background location updates, MCP config generation, Sign in with Apple + Google. |
| [pingclaw-android](https://github.com/pingclaw-me/pingclaw-android) | Kotlin / Jetpack Compose. Same thing, different platform. |

---

## Agent integration

The server generates ready-to-paste MCP config for Claude Code, Claude Desktop, VS Code, Cursor, Windsurf, and Zed. For OpenClaw and other webhook-based setups, it handles outbound POST delivery with a verifiable `Authorization: Bearer` header.

---

## Self-hosting

The server is a Go binary. If you'd rather run your own than use the hosted version at [pingclaw.me](https://pingclaw.me):

```bash
git clone https://github.com/pingclaw-me/pingclaw-server
cd pingclaw-server
cp .env.example .env
# edit .env — you need a Redis instance and your OpenClaw webhook URL
go run ./cmd/server
```

The apps point to `https://pingclaw.me` by default but accept a custom server URL in settings if you use a development build. Point the app at your own server instance.

---

## Privacy

- Location held in Redis memory only — no database writes
- 24-hour TTL, overwritten on each update
- No location history, no movement tracking
- API key stored as a hash — the raw token is shown once and never again
- All stored data viewable and deletable at any time
- Server code is here — read it if you want to verify

---

## Status

Early. The iOS app and server work. Android is in progress. The native OpenClaw node protocol integration is being researched.

Contributions welcome, especially from people with OpenClaw setups who can test against real gateway configurations.

---

## MIT

All three repos. Do whatever you want with it.

---

Built by [@christianreimer](https://github.com/christianreimer)
