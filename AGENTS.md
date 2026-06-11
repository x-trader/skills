# Agent Instructions

When working with XTrader through MCP, use the skills in `plugins/xtrader-mcp/skills`.

Default endpoint:

```text
/mcp/agent-ready/v1
```

Direct endpoint:

```text
/mcp
```

Do not use Direct MCP tools unless AgentReady v1 lacks the required capability.

Recommended skill activation order:

1. `xtrader-mcp-agent-ready-session`
2. `xtrader-mcp-agent-ready-governance`
3. `xtrader-mcp-agent-ready-catalog`
4. `xtrader-mcp-type-node-data` when type details, node schema, form data, or generic params are involved
5. `xtrader-mcp-agent-ready-graph-plan`
6. `xtrader-mcp-backtest-results` for backtest execution or result analysis
7. `xtrader-mcp-direct-fallback` only when needed
