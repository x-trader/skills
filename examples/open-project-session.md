# Example: Open Project Session

AgentReady MCP v1 endpoint: `/mcp/agent-ready/v1`

1. Call `open_project_session` with project identifier.
2. Inspect returned project/version/mode/capabilities.
3. Call `get_agent_bootstrap_context` for full bootstrap.
4. Call `describe_mcp_tooling` to read tool manifest.
5. Proceed to catalog or graph workflow based on task.
