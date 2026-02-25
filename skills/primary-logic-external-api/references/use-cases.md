# Use Cases

## Thesis Support
- Build a bull case by pulling positive high-impact records for a ticker in a time window.
- Build a bear case by pulling negative high-impact records and summarizing key downside drivers.

## Counter-Thesis and Risk
- For any bullish thesis, retrieve strongest contrary evidence first by abs impact.
- Explicitly surface signal direction conflicts and concentration risk.

## Catalyst Discovery
- Identify new high-signal developments with relevance + abs impact thresholds.
- Track multi-source confirmation using source_types filters.

## Coverage Diagnostics
- Distinguish mention-only coverage from scored signal coverage.
- Use ticker detail stats for 24h and 7d sentiment distribution.

## Monitoring Workflows
- Run recurring ticker-first pulls for watchlists.
- Store request_id and filter bundle in logs for reproducibility.
