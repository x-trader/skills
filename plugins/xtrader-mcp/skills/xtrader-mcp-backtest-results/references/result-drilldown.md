# Result Drilldown

Start broad, then narrow.

```text
get_backtest_snapshot
-> get_backtest_issues
-> get_backtest_results_summary
-> list_backtest_symbols
-> get_backtest_symbol_snapshot(symbol)
-> list_backtest_positions(symbol)
-> get_backtest_position_snapshot(positionId)
```

Use drilldown only when a summary, issue, symbol, or user question justifies it.

Avoid full position dumps. Prefer:

- top failing symbols
- positions linked to issues
- positions in a requested time range
- positions with unusual shapes/logs/results
