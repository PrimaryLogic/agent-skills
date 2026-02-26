# API Recipes

These recipes show MCP tool usage patterns. Each maps to a `primary-logic` connector tool call.

## 1) Broad Content Pull + Embedded Signal Rows
Use `search_content` with:
- `tickers`: "NVDA"
- `include`: "ticker_signals"
- `signal_min_relevance`: 0.6
- `signal_min_abs_impact`: 5

## 2) Ticker-First Ranked Pull
Use `get_ticker_content` with:
- ticker: "NVDA"
- `since`: "2026-02-24T00:00:00Z"
- `limit`: 50
- `min_relevance`: 0.6
- `min_abs_impact`: 5
- `sort_by`: "abs_impact"
- `sort_direction`: "desc"

## 3) Per-Content Signal Attribution
Use `get_content_ticker_signals` with:
- content_id: the target content ID
- `include_reasoning`: true

## 4) Ticker Summary + Signal Stats
Use `get_ticker_detail` with:
- ticker: "NVDA"
- `include_signal_stats`: true

## Pagination Loop
When `next_cursor` is present in the response, repeat the same tool call with `cursor` set to that
value. Continue until `next_cursor` is null.

## Billing + Key Health Diagnostics
1. Call `health_check` — if 402, subscription entitlement issue.
2. Call `get_usage` — verify rate-limit posture and request counts.
