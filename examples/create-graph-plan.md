# Example: Create and Apply Graph Plan

AgentReady MCP v1 endpoint: `/mcp/agent-ready/v1`

1. Ensure active session via `open_project_session`.
2. Resolve intent and search catalog for nodes/patterns.
3. Check port compatibility for desired connections.
4. Call `instantiate_graph_pattern` or build operation-based plan.
5. Call `validate_graph_plan` on the plan.
6. If validation passes, read governance requirements.
7. Satisfy snapshot/confirmation if required.
8. Call `apply_graph_plan` with validated plan id.
9. Summarize applied changes.
