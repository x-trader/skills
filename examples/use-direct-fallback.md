# Example: Use Direct MCP Fallback

**Route**: `/mcp`

**Skills**: `xtrader-mcp-agent-ready-session`, `xtrader-mcp-direct-fallback`, `xtrader-mcp-agent-ready-governance`

## Sequence

1. Attempt task on AgentReady MCP v1 — identify that backtest tools are missing.
2. Explain to user: "AgentReady v1 currently lacks backtest tools. Falling back to Direct MCP for this operation."
3. Call `connect_project` on `/mcp` to establish Direct MCP context.
4. Use the smallest required Direct tool:
   - `create_backtest` with project and version parameters
   - `wait_backtest` until completion
   - `get_backtest_snapshot` or `query_backtest_results` for results
5. Load `xtrader-mcp-backtest-results` for result summaries, issues, logs, symbols, and positions.
6. After task completes, return to `/mcp/agent-ready/v1`.
7. Call `get_current_project_context` on AgentReady to refresh session context.
8. Continue with AgentReady workflow.

## Expected Output

```
[AgentReady attempt] -> backtest tools not found in tool manifest
[fallback explained to user] -> "Using Direct MCP for backtest"
connect_project(project, version) -> context established
create_backtest -> backtestId=bt-789
wait_backtest(bt-789) -> completed
get_backtest_snapshot(bt-789) -> {summary, issues, positions}
[return to /mcp/agent-ready/v1]
get_current_project_context -> session refreshed
```

## Key Checks

- [ ] Fallback reason explained to user.
- [ ] Read-only Direct MCP tools preferred when possible.
- [ ] Direct MCP context not mixed with AgentReady session context.
- [ ] Returned to AgentReady after fallback.
- [ ] Direct MCP not called deprecated.
