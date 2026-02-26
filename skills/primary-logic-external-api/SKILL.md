---
name: investment-intelligence
description: >-
  Real-time investment context from Primary Logic — LLM-ranked relevance and
  impact signals from podcasts, articles, X/Twitter, Kalshi, Polymarket,
  earnings calls, filings, and other monitored sources across public and
  private companies.
license: Proprietary
metadata:
  author: Primary Logic
  version: "1.7"
---

# Primary Logic Investment Intelligence

Use the Primary Logic MCP tools to retrieve real-time, continuously refreshed investment context
with LLM-ranked relevance and impact signals for public and private companies.

## Activation Cues

Activate this skill when the user asks for any of:
- ticker-specific bullish or bearish evidence
- recent catalysts or risk signals
- per-content relevance or impact details by ticker
- source coverage or content visibility checks
- usage diagnostics

## What This Data Represents

- Source-normalized investment context: top podcasts, articles/news, X/Twitter, Kalshi, Polymarket,
  earnings calls, filings, and other monitored channels normalized into one feed
- LLM-heavy signal extraction: per-ticker relevance and impact scores attached to each content item
  to prioritize material developments
- Public + private company coverage: source visibility and ticker coverage for the requesting
  organization

## Available MCP Tools

Use the `primary-logic` connector tools:

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

## Hard Rules

- Never fabricate data; all claims must map to tool responses.
- Data visibility is org-scoped; if records are missing, org source visibility may be the cause.
- If a tool call fails, report the error and suggest a concrete next step.
- Use absolute timestamps in outputs when the user asks about recent windows.
- Do not claim market prices, positions, or execution events unless explicitly present in the data.
- Do not present outputs as guaranteed returns or autonomous execution instructions.
- Frame outputs as context for decision support and user-approved actions.

## Input Contract

Interpret each user request into this query plan:
1. objective: thesis_support, counter_thesis, catalyst_scan, sentiment_shift, coverage_check
2. scope:
   - tickers: list of uppercase ticker symbols
   - time window: since and until in ISO datetime format
   - source_types: optional list
3. signal filters:
   - min_relevance: 0..1
   - min_abs_impact: 0..10
   - sentiment: positive | negative | neutral
4. retrieval:
   - limit (default 50)
   - sort mode: date | abs_impact | relevance

If ticker or time window is missing for an investment query, ask one concise clarification.

## Decision Workflow

1. Validate connectivity with `health_check`.
2. Use `search_content` for broad discovery pulls.
3. Use `get_ticker_content` for signal-ranked ticker analysis.
4. Use `get_content_ticker_signals` for per-item attribution detail.
5. Use `get_ticker_detail` with `include_signal_stats=true` for summary context.
6. Use `list_sources` when visibility or source scope is ambiguous.
7. Use `get_usage` for rate-limit troubleshooting.

## Output Contract

Return structured investment output with:
1. key_findings: 3 to 7 concise bullets
2. thesis_view: one short paragraph
3. supporting_evidence: list of {content_id, ticker, impact_score, relevance_score}
4. contrary_evidence: same schema
5. catalysts: list
6. risks: list

If results are empty, return "no qualifying records" and suggest which filter to relax first.

## Query Defaults

- Default content limit: 50 unless user asks otherwise.
- Apply ticker filters whenever the user names tickers.
- For signal-heavy tasks, start with min_relevance >= 0.6 and min_abs_impact >= 5.

## References

- [Use cases](references/use-cases.md)
- [API recipes](references/api-recipes.md)
- [Response contracts](references/response-contracts.md)
- [Validation guide](references/validation.md)
