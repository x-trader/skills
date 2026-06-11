# Known Gaps

## AgentReady MCP v1 — Missing Capabilities

- **Backtest/execution tools**: AgentReady v1 currently has no backtest or execution tools. These are only available through Direct MCP (`/mcp`).
- **Package/dependency mutation tools**: `add_project_package_dependency`, `remove_project_package_dependency`, `update_all_dependencies`, etc. are Direct MCP only.
- **Type/node mutation tools**: `create_object_type`, `delete_type`, `create_visual_node`, `delete_visual_node`, etc. are Direct MCP only.
- **Raw graph read tools**: `get_graph` and `get_graph_summary` are Direct MCP only. AgentReady provides `validate_graph_plan` but not a raw graph read.
- **Confirmation tools**: `confirm_action`, `list_pending_confirmations`, `cancel_action` are Direct MCP only.
- **`create_graph_plan`**: The AgentReady tool descriptor registry defines metadata for `create_graph_plan`, but it is not currently exposed on the `/mcp/agent-ready/v1` route. Agents must use `instantiate_graph_pattern` or build plan payloads directly.

## Direct MCP — Notes

- Direct MCP has broader low-level direct mutation tools.
- Direct MCP is not deprecated; it is not the default agent endpoint.
- Direct MCP context is user-scoped, not session-isolated like AgentReady.
- `get_current_project_context` on Direct MCP returns Direct MCP context, while `get_current_project_context` on AgentReady returns AgentReady session context. Context from the two surfaces must not be mixed.
