# Use Cases

## Thesis Support
- Build a bull case by pulling positive high-impact records for a ticker in a time window.
- Build a bear case by pulling negative high-impact records and summarizing key downside drivers.
- Equip Codex, Claude Code, or OpenClaw to produce sourced thesis memos with explicit evidence tables.

## Counter-Thesis and Risk
- For any bullish thesis, retrieve strongest contrary evidence first by abs impact.
- Explicitly surface signal direction conflicts and concentration risk.
- Highlight where human review is required before any portfolio or execution changes.

## Catalyst Discovery
- Identify new high-signal developments with relevance + abs impact thresholds.
- Track multi-source confirmation using source_types filters.
- Trigger agent alerts when catalyst strength or direction shifts materially.

## Coverage Diagnostics
- Distinguish mention-only coverage from scored signal coverage.
- Use ticker detail stats for 24h and 7d sentiment distribution.
- Verify that each ticker in a strategy has sufficient source breadth before automation.

## Agentic Trading Assistant Workflows
- Run recurring ticker-first pulls for watchlists.
- Store request_id and filter bundle in logs for reproducibility.
- Feed validated API outputs into user-controlled trade-planning or paper-trading pipelines.
