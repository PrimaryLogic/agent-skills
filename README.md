# Primary Logic Investment Intelligence Plugin

An investment intelligence plugin for [Claude Code](https://claude.ai/code) and [Cowork](https://claude.com/product/cowork). Provides real-time, LLM-ranked signals from podcasts, articles, X/Twitter, prediction markets, earnings calls, filings, and other monitored sources across public and private companies.

> **Important**: This plugin provides investment context for decision support. All outputs should be reviewed by qualified professionals before use in investment decisions.

## Installation

### Claude Code Plugin

```bash
claude plugins add PrimaryLogic/agent-skills
```

### npx (Agent Skills)

```bash
npx skills add PrimaryLogic/agent-skills
```

Or install directly into Claude Code:

```bash
npx skills add PrimaryLogic/agent-skills --agent claude-code --skill '*' -y --copy
```

## Prerequisites

1. Log in at [primarylogic.com](https://www.primarylogic.com).
2. Ensure you have an active API-tier subscription.
3. Create an API key from **Settings -> API Keys** in the dashboard.

## Skills

| Skill | Description |
|-------|-------------|
| `investment-intelligence` | MCP-powered investment context — ticker-specific bull/bear evidence, catalyst/risk signals, source coverage, and per-content ticker attribution via structured MCP tools |
| `primary-logic-external-api` | Raw HTTP API reference for the `/v1` endpoints — use for non-MCP agents or direct API integration |

## MCP Integration

> If you need to check which tools are connected, see [CONNECTORS.md](plugin/CONNECTORS.md).

The plugin includes a remote MCP server (`.mcp.json`) that provides structured tools for querying investment data. Set `PRIMARYLOGIC_API_KEY` in your environment and the connector authenticates automatically.

### Available MCP Tools

| Tool | Purpose |
|------|---------|
| `health_check` | Validate connectivity and auth |
| `search_content` | Broad content discovery with filters (tickers, sources, sentiment, time) |
| `get_content` | Fetch a single content item by ID |
| `get_content_ticker_signals` | Per-item ticker attribution with relevance and impact |
| `get_ticker_content` | Signal-ranked content for a specific ticker |
| `list_sources` | Org source visibility and coverage |
| `list_tickers` | Search available tickers |
| `get_ticker_detail` | Ticker summary with optional signal stats |
| `get_usage` | API usage telemetry |

## Example Usage Prompts

- `Build a bull and bear case for NVDA from the last 7 days with the highest-impact evidence first.`
- `Show contradictory evidence for MSFT with relevance >= 0.6 and abs impact >= 5.`
- `Check whether my org has source coverage gaps for AMD-related content.`
- `Diagnose why my external API key is not returning ticker signals.`

## Repository Structure

```text
agent-skills/
├── .claude-plugin/
│   └── marketplace.json          # Marketplace manifest (points to plugin/)
├── plugin/                       # Cowork plugin (MCP-only skill)
│   ├── .claude-plugin/plugin.json
│   ├── .mcp.json
│   ├── CONNECTORS.md
│   └── skills/
│       └── investment-intelligence/
│           └── SKILL.md
├── skills/                       # npx skills add (all skills)
│   ├── investment-intelligence/
│   │   └── SKILL.md
│   └── primary-logic-external-api/
│       ├── SKILL.md
│       └── references/
└── README.md
```
