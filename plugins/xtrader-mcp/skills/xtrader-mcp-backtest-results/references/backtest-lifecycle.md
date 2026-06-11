# Backtest Lifecycle

Use Direct MCP only after explaining that AgentReady MCP v1 does not expose backtest tools.

## New Backtest

```text
connect_project
-> create_backtest
-> wait_backtest
-> get_backtest_overview
-> get_backtest_snapshot
-> get_backtest_issues
-> get_backtest_results_summary
```

## Existing Backtest

```text
connect_project
-> list_backtests
-> get_backtest
-> get_backtest_overview
-> get_backtest_snapshot
-> get_backtest_issues
```

If the backtest is still running, use `wait_backtest` before deep result analysis.

Return to AgentReady MCP v1 after backtest work and refresh context.
