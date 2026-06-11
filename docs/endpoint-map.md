# Endpoint Map

| Route | Surface | Default? | Authorization | Tool Availability |
|---|---|---|---|---|
| `/mcp` | Direct MCP | No | Required | 92 Direct MCP tools |
| `/mcp/agent-ready/v1` | AgentReady MCP v1 | Yes | Required | 13 AgentReady tools |

## Rules

- `/mcp/agent-ready/v1` is the default endpoint for agents.
- `/mcp` is a controlled fallback / trusted low-level surface.
- Both endpoints require authorization.
- Each endpoint exposes a different tool set.
- Agents should choose the endpoint by workflow need, not by internal server details.
