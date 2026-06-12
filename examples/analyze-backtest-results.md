# Example: Analyze Backtest Results

**Endpoint**: `/mcp` through controlled Direct fallback.

**Skills**: `xtrader-session`, `xtrader-backtests`, `xtrader-direct`

## Sequence

1. Start from AgentReady context and explain fallback.
2. Call `connect_project` on `/mcp`.
3. Call `list_backtests` or `get_backtest` to select a backtest.
4. Call `get_backtest_overview` for status/progress.
5. Call `get_backtest_snapshot` for compact result context.
6. Call `get_backtest_issues` for normalized problems.
7. Call `get_backtest_results_summary` for aggregate symbol results.
8. Use `get_backtest_timeline` only if time-distribution matters.
9. Drill into symbols/positions only if the summary or user request requires it.

## Summary Shape

```text
Status: completed / running / failed
Coverage: symbols processed, positions counted
Outcome: win/loss or result aggregates where available
Issues: top normalized issues
Focus: symbols or positions that need investigation
Next steps: targeted follow-up queries or graph review suggestions
```

## Key Checks

- [ ] Summary tools used before raw tools.
- [ ] Issues included in analysis.
- [ ] Claims supported by MCP result data.
- [ ] No raw payload dump.
