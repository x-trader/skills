# Eval: Direct MCP Fallback

**Skills under test**: `xtrader-mcp-agent-ready-session`, `xtrader-mcp-direct-fallback`

## Scenario

User asks: "Run a backtest on my current strategy to see how it performed last month."

Note: AgentReady MCP v1 currently lacks backtest tools.

## Expected Agent Behavior

1. Identify that AgentReady v1 lacks backtest capability.
2. Explain why Direct MCP fallback is needed.
3. Connect via Direct MCP `/mcp`.
4. Use the smallest required Direct MCP tool (`create_backtest`, `wait_backtest`, `get_backtest_snapshot`).
5. After backtest completes, return to AgentReady MCP v1.
6. Refresh AgentReady context with `get_current_project_context`.
7. Do not mix Direct MCP context with AgentReady session context.

## Pass/Fail Rubric

| Criteria | Pass | Fail |
|---|---|---|
| Default endpoint | Starts on AgentReady v1 | Uses Direct MCP as first choice |
| Fallback explanation | Explains which capability is missing | Falls back without explanation |
| Tool selection | Uses smallest required tool | Uses broad or unnecessary Direct tools |
| Context isolation | Returns to AgentReady after fallback | Stays on Direct MCP |
| Not deprecated | Never calls Direct MCP deprecated | Calls Direct MCP deprecated |
| Skill activation | Loads `xtrader-mcp-direct-fallback` | Falls back without loading the skill |

## Negative Cases

| Case | Expected behavior |
|---|---|
| Agent connects directly to `/mcp` without trying AgentReady | Fail — must prefer AgentReady |
| Agent falls back silently without explaining why | Fail — must explain fallback reason |
| Agent uses `replace_graph` on Direct MCP for a backtest task | Fail — must use the smallest tool |
| Agent stays on Direct MCP after backtest completes | Fail — must return to AgentReady |
| Agent mixes `get_current_project_context` from both surfaces | Fail — context isolation required |
| Agent calls Direct MCP "legacy" or "deprecated" | Fail — Direct MCP is not deprecated |
