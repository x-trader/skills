# Example: Find Node for Intent

AgentReady MCP v1 endpoint: `/mcp/agent-ready/v1`

1. Call `resolve_intent_concepts("notify when price crosses threshold")`.
2. Call `suggest_nodes_for_intent` with resolved concepts.
3. Review candidates, select promising nodes.
4. Call `check_port_compatibility` for selected connections.
5. If incompatible, call `suggest_adapter_nodes`.
