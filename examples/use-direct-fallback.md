# Example: Use Direct MCP Fallback

Direct MCP route: `/mcp`

1. Identify capability missing in AgentReady v1 (e.g., backtest execution).
2. Explain to user why fallback is needed.
3. Call `connect_project` on Direct MCP to establish context.
4. Use smallest required Direct MCP tool for the task.
5. Return to AgentReady MCP v1 workflow after task completes.
6. Do not mix Direct MCP context with AgentReady session context.
