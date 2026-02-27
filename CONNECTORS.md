# Connectors

## Connectors for this plugin

| Category | Placeholder | Included servers |
|----------|-------------|-----------------|
| Investment intelligence | `~~investment-intelligence` | Primary Logic |

The Primary Logic MCP server provides real-time, LLM-ranked investment context from monitored sources including podcasts, articles, X/Twitter, Kalshi, Polymarket, earnings calls, and filings.

## Authentication

The connector authenticates via OAuth only. Use the OAuth metadata endpoints and complete the auth flow in your MCP client:
- `GET /.well-known/oauth-protected-resource`
- `GET /.well-known/oauth-authorization-server`
- `POST /oauth/token`
