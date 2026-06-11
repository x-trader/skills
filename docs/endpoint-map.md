# Endpoint Map

| Route | Surface | Default? | Authorization | Tool Filtering |
|---|---|---|---|---|
| `/mcp` | Direct MCP | No | Required | 104 Direct MCP tools |
| `/mcp/agent-ready/v1` | AgentReady MCP v1 | Yes | Required | 13 AgentReady tools |

## Rules

- `/mcp/agent-ready/v1` is the default endpoint for agents.
- `/mcp` is a controlled fallback / trusted low-level surface.
- Both endpoints require authorization.
- Tools are filtered at runtime by route path in `Router.cs:FilterToolsForRequestPath`.
- The same server binary serves both endpoints; capability differs only by allowed tool set.
