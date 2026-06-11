# Example: Live Protected Change

AgentReady MCP v1 endpoint: `/mcp/agent-ready/v1`

1. Ensure active session and read project mode (LiveProtected).
2. Call `describe_mcp_tooling` to check risk metadata.
3. Build or instantiate graph plan with small, surgical changes.
4. Call `validate_graph_plan`.
5. Create snapshot if policy requires.
6. Require user confirmation before apply.
7. Call `apply_graph_plan` only after confirmation.
8. Verify applied changes with `get_current_project_context`.
