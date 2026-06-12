# Eval: Backtest Results

**Skills under test**: `xtrader-session`, `xtrader-backtests`, `xtrader-direct`

## Scenario

User asks: "Run a backtest on my current project and tell me why the worst symbol performed badly."

## Expected Agent Behavior

1. Starts from AgentReady session context.
2. Loads `xtrader-backtests`.
3. Explains Direct MCP fallback because AgentReady v1 lacks backtest tools.
4. Calls `connect_project` on `/mcp`.
5. Calls `create_backtest`, then `wait_backtest`.
6. Calls `get_backtest_overview`, `get_backtest_snapshot`, `get_backtest_issues`, and `get_backtest_results_summary`.
7. Identifies the worst symbol from summary/issues.
8. Uses focused drilldown: `get_backtest_symbol_snapshot`, selected positions, and focused logs.
9. Summarizes findings without dumping full logs/positions.
10. Returns to AgentReady and refreshes context.

## Pass/Fail Rubric

| Criteria | Pass | Fail |
|---|---|---|
| Skill activation | Loads `xtrader-backtests` | Uses only `xtrader-direct` |
| Fallback explanation | Explains AgentReady lacks backtest tools | Uses `/mcp` silently |
| Lifecycle | Creates and waits/polls backtest | Creates but does not wait/poll |
| Summary first | Uses overview/snapshot/issues/summary before drilldown | Starts with full logs or all positions |
| Issues | Calls `get_backtest_issues` | Ignores issues |
| Drilldown | Narrows to symbol/position/time range | Dumps all symbols/positions/logs |
| Scope | Does not mutate graph/type/package state | Mutates project state during analysis |
| Return | Refreshes AgentReady context after fallback | Stays on Direct MCP |

## Negative Cases

| Case | Expected behavior |
|---|---|
| Agent uses Direct MCP without explaining fallback | Fail — fallback reason required |
| Agent dumps full logs into response | Fail — use focused excerpts only |
| Agent creates a backtest but never calls `wait_backtest` | Fail — must poll or check completion |
| Agent analyzes results without `get_backtest_issues` | Fail — issues are required |
| Agent edits graph based on result findings | Fail — propose separate governed workflow |
