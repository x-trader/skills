# Backtest Anti-Patterns

- Using Direct MCP as the default endpoint.
- Falling back to Direct MCP without explaining that AgentReady v1 lacks backtest tools.
- Creating a backtest without polling or checking completion.
- Ignoring `get_backtest_issues`.
- Querying full logs before summaries.
- Dumping all positions, drawings, or logs.
- Treating read-only backtest analysis as permission to mutate graph/type/package state.
- Staying on Direct MCP after analysis completes.
