# Primary Logic Investment Intelligence Plugin

An investment intelligence plugin for AI coding agents. Provides real-time, LLM-ranked signals from podcasts, articles, X/Twitter, prediction markets, earnings calls, filings, and other monitored sources across public and private companies.

> **Important**: This plugin provides investment context for decision support. All outputs should be reviewed by qualified professionals before use in investment decisions.

## Installation

### Cowork

1. Open **Manage Plugins**.
2. Click **Personal** -> **Add a Marketplace from GitHub**.
3. Enter `PrimaryLogic/agent-skills`.
4. Install the plugin, click **Manage**, then connect the `primary-logic` connector.
5. Run `/primary-logic give me an update about NVDA`.
6. If prompted, complete OAuth.

### OpenClaw

Paste this into OpenClaw:
```text
Install the plugin https://github.com/PrimaryLogic/agent-skills and run the Oauth flow
```

### Claude Code

```bash
claude plugin marketplace add PrimaryLogic/agent-skills
claude plugin install primary-logic
```

Claude prompts for OAuth automatically on first tool call.

### Codex

```bash
codex mcp add primary-logic --url https://primarylogic--pulse-backend-external-api-app.modal.run/mcp
```

### Other MCP-capable agents

Add to your agent's MCP config:
- URL: `https://primarylogic--pulse-backend-external-api-app.modal.run/mcp`
- Auth: OAuth only (authorization_code + PKCE for interactive clients, client_credentials for user-owned bots)

### npx (universal)

```bash
npx skills add PrimaryLogic/agent-skills
```

## Prerequisites

1. Log in at [primarylogic.com](https://www.primarylogic.com).
2. Ensure you have an active Automation-tier subscription.
3. Complete OAuth setup from **Settings -> OAuth** (`/api-keys` route).

## MCP Tools

> If you need to check which tools are connected, see [CONNECTORS.md](CONNECTORS.md).

The plugin includes a remote MCP server (`.mcp.json`) that provides structured tools for querying investment data. Authentication is handled via OAuth.

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
- `Diagnose why my OAuth token is not returning ticker signals.`

## Repository Structure

```text
agent-skills/
├── .claude-plugin/
│   ├── marketplace.json
│   └── plugin.json
├── .mcp.json
├── CONNECTORS.md
├── README.md
└── skills/
    └── primary-logic/
        ├── SKILL.md
        └── references/
            ├── api-recipes.md
            ├── response-contracts.md
            └── use-cases.md
```
