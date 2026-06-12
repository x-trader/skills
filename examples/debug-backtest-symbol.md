# Example: Debug Backtest Symbol

**Endpoint**: `/mcp` through controlled Direct fallback.

**Skills**: `xtrader-backtests`, `xtrader-direct`

## Sequence

1. Use `get_backtest_snapshot` to identify candidate symbols.
2. Call `list_backtest_symbols` if symbol selection is needed.
3. Call `get_backtest_symbol_snapshot(symbol)` for focused symbol context.
4. Call `get_backtest_positions_summary(symbol)`.
5. Call `list_backtest_positions(symbol)` only with limits or filters.
6. Call `get_backtest_position_snapshot(positionId)` for selected positions.
7. Call `search_backtest_logs(query)` for focused log search.
8. Call `list_backtest_logs(symbol, timeRange)` only if targeted excerpts are needed.
9. Summarize high-signal findings.

## Key Checks

- [ ] Symbol drilldown justified by summary/issues.
- [ ] Position drilldown limited and focused.
- [ ] Logs searched before listing.
- [ ] Only relevant log excerpts cited.
- [ ] No graph/type/package mutation during debugging.
