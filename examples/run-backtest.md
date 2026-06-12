# Example: Run Backtest

**Endpoint**: start with `/mcp/agent-ready/v1`; use `/mcp` because backtest tools are Direct MCP-only.

**Skills**: `xtrader-session`, `xtrader-backtests`, `xtrader-direct`

## Sequence

1. Verify active AgentReady session with `get_current_project_context`.
2. Explain Direct fallback: AgentReady v1 does not expose backtest tools.
3. Call `connect_project` on `/mcp`.
4. Call `create_backtest` with bounded parameters.
5. Call `wait_backtest` until complete or timeout.
6. Call `get_backtest_overview`.
7. Call `get_backtest_snapshot`.
8. Call `get_backtest_issues`.
9. Call `get_backtest_results_summary`.
10. Summarize results and return to AgentReady.

## Key Checks

- [ ] Direct fallback reason explained.
- [ ] Backtest was waited/polled after creation.
- [ ] Overview/snapshot/issues read before drilldown.
- [ ] No full logs or positions dumped.
- [ ] Returned to AgentReady after Direct MCP use.
