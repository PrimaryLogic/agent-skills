# Response Contracts

## Common Envelope
```json
{
  "data": {},
  "next_cursor": 50,
  "request_id": "req_123",
  "generated_at": "2026-02-25T12:00:00+00:00"
}
```

## Content Item
```json
{
  "id": "c1",
  "date": "2026-02-25T10:00:00+00:00",
  "source_type": "Article",
  "ticker_mentioned_primary": ["NVDA"],
  "tickers_related": ["MSFT"],
  "kg_relevant_tickers": ["NVDA", "MSFT"],
  "summary": "Guidance raise with accelerating demand.",
  "base_relevance": 0.82,
  "primary_impact_score": 0.7,
  "sentiment": "positive",
  "ticker_signals": []
}
```

## Ticker Signal Row
```json
{
  "ticker": "NVDA",
  "in_primary": true,
  "primary_rank": 1,
  "in_related": false,
  "related_rank": null,
  "in_kg_relevant": true,
  "kg_relevant_rank": 1,
  "relevance_score": 0.81,
  "impact_score": 7,
  "sentiment": "positive",
  "relevance_reasoning": null,
  "impact_reasoning": null
}
```

## Ticker-First Item
```json
{
  "content": {"id": "c1", "date": "2026-02-25T10:00:00+00:00", "summary": "..."},
  "ticker_signal": {"ticker": "NVDA", "relevance_score": 0.81, "impact_score": 7}
}
```

## Agent Output Example
```json
{
  "key_findings": ["NVDA has two high-impact records in the last 24h."],
  "thesis_view": "Signal balance is net positive with notable downside counter-evidence.",
  "supporting_evidence": [{"content_id": "c1", "ticker": "NVDA", "impact_score": 7, "relevance_score": 0.81}],
  "contrary_evidence": [{"content_id": "c2", "ticker": "NVDA", "impact_score": -8, "relevance_score": 0.66}],
  "catalysts": ["Raised guidance"],
  "risks": ["Supply constraints"],
  "api_trace": {
    "endpoints": ["/v1/tickers/NVDA/content"],
    "filters": {"min_relevance": 0.6, "min_abs_impact": 5},
    "time_window": {"since": "2026-02-24T00:00:00Z", "until": "2026-02-25T00:00:00Z"},
    "pagination_covered": true
  }
}
```
