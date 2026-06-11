# Endpoint Map

| Route              | Surface             | Default? | Usage                                    |
|--------------------|---------------------|----------|------------------------------------------|
| `/mcp`             | Direct MCP          | No       | Controlled fallback when AgentReady lacks capability |
| `/mcp/agent-ready/v1` | AgentReady MCP v1 | Yes      | Default agent endpoint                   |

## Summary

- `/mcp/agent-ready/v1` is the default endpoint for agents.
- `/mcp` (Direct MCP) is a controlled fallback / trusted low-level surface.
- Agents should prefer AgentReady MCP v1 and fall back to Direct MCP only when necessary.
