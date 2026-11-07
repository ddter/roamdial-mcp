# RoamDial MCP Server — Live World Radio on a 3D Globe

[![Glama MCP Connector](https://glama.ai/mcp/connectors/io.github.DDTer/roamdial/badges/score.svg)](https://glama.ai/mcp/connectors/io.github.DDTer/roamdial)
[![MCP Registry](https://img.shields.io/badge/MCP_Registry-io.github.ddter%2Froamdial-blue)](https://registry.modelcontextprotocol.io/v0.1/servers/io.github.ddter%2Froamdial/versions/latest)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](./LICENSE)
[![Website](https://img.shields.io/badge/Live_3D_Globe-roamdial.com-ff6b35)](https://roamdial.com)

**[RoamDial](https://roamdial.com)** is a free, ad-free interactive 3D world radio map with **35,000+ verified live radio streams across 215 countries and territories**.

This repository provides the official **Model Context Protocol (MCP)** integration for RoamDial:
1. **Direct Remote Streamable HTTP Server (`https://roamdial.com/mcp`)** — zero install, no API key or authentication required.
2. **Lightweight Local `stdio` Bridge (`npx -y github:ddter/roamdial-mcp`)** — zero-dependency Node.js wrapper for local-only MCP clients.

---

## Quick Start

### Option 1: Remote Streamable HTTP (Recommended — Zero Install)

Point any MCP client supporting **Streamable HTTP** (`2025-06-18` / `2025-03-26` / `2026-07-28`) directly at:

```text
https://roamdial.com/mcp
```

#### Claude Code
```bash
claude mcp add --transport http roamdial https://roamdial.com/mcp
```

#### Cursor / VS Code / Windsurf (`mcp.json`)
```json
{
  "mcpServers": {
    "roamdial": {
      "url": "https://roamdial.com/mcp"
    }
  }
}
```

#### OpenAI Codex (`~/.codex/config.toml`)
```toml
[mcp_servers.roamdial]
url = "https://roamdial.com/mcp"
```

#### ChatGPT / Claude.ai Web Connectors
Add `https://roamdial.com/mcp` under **Settings → Connectors** (no authentication required).

---

### Option 2: Local `stdio` Bridge (`claude_desktop_config.json`)

For MCP clients that only support local `stdio` processes (requires Node.js >= 18):

```json
{
  "mcpServers": {
    "roamdial": {
      "command": "npx",
      "args": ["-y", "github:ddter/roamdial-mcp"]
    }
  }
}
```

---

## Available MCP Tools (4 Tools)

All tools are read-only, require no authentication, and return both human-readable Markdown (`content`) and machine-typed JSON (`structuredContent` + `outputSchema`), including direct one-click listening URLs (`listenUrl` and 3D globe `mapUrl`).

### 1. `search_stations`
Search live radio stations across 35,000+ verified streams by keyword, country, city, genre, or language.
- **Parameters**:
  - `query` *(string, optional)*: Station name, callsign, frequency, city, or keyword (e.g. `"BBC"`, `"Jazz"`, `"Tokyo"`, `"KEXP"`).
  - `country` *(string, optional)*: ISO-2 country code, country slug, or country name (e.g. `"JP"`, `"united-kingdom"`, `"Brazil"`).
  - `city` *(string, optional)*: City name filter (e.g. `"Paris"`, `"New York"`, `"Seoul"`).
  - `genre` *(string, optional)*: Genre slug or keyword (e.g. `"jazz"`, `"classical"`, `"news"`, `"electronic"`, `"rock"`, `"ambient"`).
  - `language` *(string, optional)*: Broadcast language filter (e.g. `"English"`, `"Japanese"`, `"French"`).
  - `limit` *(integer, optional, 1–20, default 10)*: Maximum stations to return.

### 2. `spin_globe`
Spin the 3D globe and land on a random live radio station, optionally constrained by country, genre, or mood/time-of-day, and probe its live ICY track title.
- **Parameters**:
  - `country` *(string, optional)*: ISO-2 code, slug, or country name.
  - `genre` *(string, optional)*: Genre slug or keyword.
  - `mood` *(enum, optional)*:
    - `"late_night"` — stations where local time at the broadcast city is currently **22:00–04:00**
    - `"morning"` — stations where local time at the broadcast city is currently **06:00–10:00**
    - `"focus"` — instrumental / ambient / classical / jazz / lo-fi stations
    - `"upbeat"` — pop / rock / dance / electronic / latin / hip-hop stations
    - `"relax"` — chill / easy listening / ambient / acoustic / smooth jazz stations

### 3. `get_station`
Get the full profile of a station by its 12-hex ID or `slug-id`, including broadcast location, local time, stream codec/bitrate, Wikipedia background, RoamDial listener stats, live ICY track metadata, and similar stations.
- **Parameters**:
  - `stationId` *(string, required)*: 12-character hex ID (e.g. `"961bf53d0601"`) or station slug (`"bbc-radio-3-961bf53d0601"`).

### 4. `get_now_playing`
Query the live ICY `StreamTitle` metadata currently broadcasting on a station (with explicit `observedAt` timestamp and availability reason).
- **Parameters**:
  - `stationId` *(string, required)*: 12-character hex ID or `slug-id`.

---

## Example Prompts to Try

- *"Find me a late-night jazz radio station broadcasting live right now where it's past midnight local time, and tell me what song is playing."*
- *"Search for live radio stations in Tokyo or Kyoto and give me direct links to listen."*
- *"Spin the globe to a random morning radio show somewhere in the world."*
- *"What is currently playing on KEXP or BBC Radio 3?"*

---

## Additional AI & Discovery Endpoints

- **3D World Radio Map**: [https://roamdial.com](https://roamdial.com)
- **RFC 9727 API Catalog**: [https://roamdial.com/.well-known/api-catalog](https://roamdial.com/.well-known/api-catalog)
- **OpenAPI 3.1 Specification (for Custom GPT Actions)**: [https://roamdial.com/openapi.json](https://roamdial.com/openapi.json)
- **LLMs Summary (`llms.txt`)**: [https://roamdial.com/llms.txt](https://roamdial.com/llms.txt)
- **LLMs Full Curated Catalog (`llms-full.txt`)**: [https://roamdial.com/llms-full.txt](https://roamdial.com/llms-full.txt)

---

## License

[MIT](./LICENSE) © [RoamDial](https://roamdial.com)
