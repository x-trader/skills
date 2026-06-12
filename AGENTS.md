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

1. `xtrader-session`
2. `xtrader-governance`
3. `xtrader-catalog`
4. `xtrader-types` when type details, object/enum types, compatibility, or type mutation are involved
5. `xtrader-nodes` when node schema, form data, input values, generic params, or array port types are involved
6. `xtrader-visual-graphs` when VisualNode, FlowGraph, nested visual nodes, public port nodes, or port kinds are involved
7. `xtrader-graph-plan`
8. `xtrader-backtests` for backtest execution or result analysis
9. `xtrader-direct` only when needed
