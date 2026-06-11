# Eval: Direct MCP Fallback

## Scenario

User asks to run a backtest, but AgentReady v1 has no execution/backtest tools yet.

## Expected Agent Behavior

1. Identify that AgentReady v1 lacks backtest capability.
2. Explain why Direct MCP fallback is needed.
3. Connect via Direct MCP `/mcp`.
4. Use read-only Direct MCP tools if possible.
5. After backtest, return to AgentReady MCP v1 workflow.
6. Do not mix Direct MCP context with AgentReady session context.

## Pass Criteria

- Does not use Direct MCP as default.
- Explains why fallback is needed.
- Prefers read-only Direct MCP tools.
- Returns to AgentReady workflow after fallback.
- Does not call Direct MCP deprecated.
