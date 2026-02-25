# API Recipes

Assume:
- BASE=https://primarylogic--pulse-backend-external-api-app.modal.run
- KEY=<PRIMARYLOGIC_API_KEY>

## 1) Broad Content Pull + Embedded Signal Rows
```bash
curl -s -H "Authorization: Bearer $KEY" \
  "$BASE/v1/content?tickers=NVDA&include=ticker_signals&signal_min_relevance=0.6&signal_min_abs_impact=5"
```

## 2) Ticker-First Ranked Pull
```bash
curl -s -H "Authorization: Bearer $KEY" \
  "$BASE/v1/tickers/NVDA/content?since=2026-02-24T00:00:00Z&limit=50&min_relevance=0.6&min_abs_impact=5&sort_by=abs_impact&sort_direction=desc"
```

## 3) Per-Content Signal Attribution
```bash
curl -s -H "Authorization: Bearer $KEY" \
  "$BASE/v1/content/CONTENT_ID/ticker-signals?include_reasoning=true"
```

## 4) Ticker Summary + Signal Stats
```bash
curl -s -H "Authorization: Bearer $KEY" \
  "$BASE/v1/entities/tickers/NVDA?include_signal_stats=true"
```

## Pagination Loop
```bash
CURSOR=0
while [ "$CURSOR" != "null" ]; do
  RESP=$(curl -s -H "Authorization: Bearer $KEY" "$BASE/v1/content?cursor=$CURSOR&limit=100")
  echo "$RESP" | jq '.data | length'
  CURSOR=$(echo "$RESP" | jq '.next_cursor')
done
```

## Billing + Key Health Diagnostics
```bash
curl -s -H "Authorization: Bearer $KEY" "$BASE/v1/health"
curl -s -H "Authorization: Bearer $KEY" "$BASE/v1/usage"
```
