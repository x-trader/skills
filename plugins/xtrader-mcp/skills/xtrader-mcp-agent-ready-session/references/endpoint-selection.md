# Endpoint Selection

| Route | Surface | Role |
|---|---|---|
| `/mcp/agent-ready/v1` | AgentReady MCP v1 | Default — isolated session, governed tools, semantic catalog |
| `/mcp` | Direct MCP | Fallback — user-scoped context, broader tool set, direct mutation |

Choose AgentReady MCP v1 by default. Use Direct MCP only when:

1. AgentReady v1 does not expose the required capability.
2. The task requires backtest, package mutation, type mutation, or raw graph read tools.
3. Confirmation tools (`confirm_action`) are needed and AgentReady does not expose them.

When falling back to Direct MCP, always explain why and return to AgentReady after the task.
