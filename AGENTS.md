# Agent Instructions

When working with XTrader through MCP, use the skills in `plugins/xtrader-mcp/skills`.

Default endpoint:

```text
/mcp/agent-ready/v1
```

Legacy endpoint:

```text
/mcp
```

Do not use legacy tools unless AgentReady v1 lacks the required capability.

Recommended skill activation order:

1. `xtrader-mcp-agent-ready-session`
2. `xtrader-mcp-agent-ready-governance`
3. `xtrader-mcp-agent-ready-catalog`
4. `xtrader-mcp-agent-ready-graph-plan`
5. `xtrader-mcp-legacy-interop` only when needed
