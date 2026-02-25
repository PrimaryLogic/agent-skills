---
name: primary-logic-external-api
description: >-
  Query the Primary Logic External API under /v1 for investment intelligence from
  standardized_content and standardized_content_tickers. Use when asked to pull
  thesis evidence, ticker signals, source coverage, or API usage telemetry.
license: Proprietary
compatibility: Requires internet access and HTTPS calls with Authorization bearer headers.
metadata:
  author: primary-logic
  version: "1.3"
---

# Primary Logic External API

Use this skill to retrieve read-only investment intelligence from the Primary Logic External API.

## Activation Cues
Activate this skill when the user asks for any of:
- ticker-specific bullish or bearish evidence
- recent catalysts or risk signals from content
- per-content relevance or impact details by ticker
- source coverage or content visibility checks
- API key usage diagnostics for external data pulls

## Data Surfaces
- standardized_content:
  - normalized content rows (summary, snippet, source metadata, tickers)
- standardized_content_tickers:
  - per-content, per-ticker signal rows (relevance, impact, signal flags, optional reasoning)

## Connection
- Base URL: https://primarylogic--pulse-backend-external-api-app.modal.run
- Auth header: Authorization: Bearer <PRIMARYLOGIC_API_KEY>
- API path scope: /v1 only

## Hard Rules
- Only call read-only GET endpoints under /v1.
- Never fabricate data; all claims must map to API responses.
- Data is org-scoped; if records are missing, org visibility may be the cause.
- If an API call fails, report status, error code or message, and a concrete next step.
- Use absolute timestamps in outputs when the user asks about recent windows.
- Do not claim market prices, positions, or execution events unless explicitly present in the API data.

## Input Contract
Interpret each user request into this query plan:
1. objective:
   - thesis_support, counter_thesis, catalyst_scan, sentiment_shift, coverage_check
2. scope:
   - tickers: list of uppercase ticker symbols
   - time window: since and until in ISO datetime format
   - source_types: optional list
3. signal filters:
   - min_relevance: 0..1
   - min_abs_impact: 0..10
   - sentiment: positive|negative|neutral
   - include_reasoning: true when the user asks why
4. retrieval:
   - limit (default 50)
   - sort mode: date|abs_impact|relevance

If ticker or time window is missing for an investment decision request, ask one concise clarification.

## Query Defaults
- Default content limit: 50 unless user asks otherwise.
- Apply ticker filters whenever the user names tickers.
- For larger pulls, continue pagination while next_cursor is present.
- For signal-heavy tasks, start with min_relevance >= 0.6 and min_abs_impact >= 5.

## Data Shape (API Output)
See [response contracts](references/response-contracts.md) for canonical payload examples.

## Output Contract
Return structured investment output with:
1. key_findings: 3 to 7 concise bullets
2. thesis_view: one short paragraph
3. supporting_evidence: list of {content_id, ticker, impact_score, relevance_score}
4. contrary_evidence: same schema as supporting_evidence
5. catalysts: list
6. risks: list
7. api_trace:
   - endpoints used
   - filters used
   - time window
   - pagination coverage

If results are empty, return "no qualifying records" and suggest exactly which filter to relax first.

## Decision Workflow
1. Validate connectivity once per session with GET /v1/health.
2. Use GET /v1/content for broad discovery pulls.
3. Use GET /v1/tickers/{ticker}/content for signal-ranked ticker analysis.
4. Use GET /v1/content/{content_id}/ticker-signals for per-item attribution detail.
5. Use GET /v1/entities/tickers/{ticker}?include_signal_stats=true for summary context.
6. Use GET /v1/sources when visibility or source scope is ambiguous.
7. Use GET /v1/usage for telemetry and rate-limit troubleshooting.

## Endpoint Cheat Sheet
- GET https://primarylogic--pulse-backend-external-api-app.modal.run/v1/health
- GET https://primarylogic--pulse-backend-external-api-app.modal.run/v1/content
- GET https://primarylogic--pulse-backend-external-api-app.modal.run/v1/content/{content_id}
- GET https://primarylogic--pulse-backend-external-api-app.modal.run/v1/content/{content_id}/ticker-signals
- GET https://primarylogic--pulse-backend-external-api-app.modal.run/v1/tickers/{ticker}/content
- GET https://primarylogic--pulse-backend-external-api-app.modal.run/v1/sources
- GET https://primarylogic--pulse-backend-external-api-app.modal.run/v1/entities/tickers
- GET https://primarylogic--pulse-backend-external-api-app.modal.run/v1/entities/tickers/{ticker}
- GET https://primarylogic--pulse-backend-external-api-app.modal.run/v1/usage

## Quick Connectivity Test
```bash
curl -s \
  -H "Authorization: Bearer <PRIMARYLOGIC_API_KEY>" \
  "https://primarylogic--pulse-backend-external-api-app.modal.run/v1/health"
```

## References
- [Use cases](references/use-cases.md)
- [API recipes](references/api-recipes.md)
- [Response contracts](references/response-contracts.md)
- [Validation guide](references/validation.md)
