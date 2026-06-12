# Known Gaps

## AgentReady MCP v1 — Missing Capabilities

- **Backtest/execution tools**: AgentReady v1 currently has no backtest or execution tools. These are only available through Direct MCP (`/mcp`); use `xtrader-backtests` for these workflows.
- **Package/dependency mutation tools**: `add_project_package_dependency`, `remove_project_package_dependency`, `update_all_dependencies`, etc. are Direct MCP only.
- **Type/node mutation tools**: `create_object_type`, `delete_type`, `create_visual_node`, `delete_visual_node`, etc. are Direct MCP only.
- **Full type/node details**: `get_type_details`, `get_type_form_schema`, and `get_node_details` are Direct MCP only.
- **Node data mutation**: `set_node_form_data`, `set_input_port_value`, `set_type_param`, and `set_array_port_types` are Direct MCP only unless represented through a supported AgentReady graph plan payload.
- **Raw graph read tools**: `get_graph` and `get_graph_summary` are Direct MCP only. AgentReady provides `validate_graph_plan` but not a raw graph read.
- **Confirmation tools**: `confirm_action`, `list_pending_confirmations`, `cancel_action` are Direct MCP only.
- **Graph plan creation**: AgentReady v1 exposes `instantiate_graph_pattern`, `validate_graph_plan`, and `apply_graph_plan`, but does not expose a separate `create_graph_plan` tool. Agents must use pattern instantiation or build supported plan payloads directly.

## Direct MCP — Notes

- Direct MCP has broader low-level direct mutation tools.
- Direct MCP is not deprecated; it is not the default agent endpoint.
- Direct MCP context is user-scoped, not session-isolated like AgentReady.
- `get_current_project_context` on Direct MCP returns Direct MCP context, while `get_current_project_context` on AgentReady returns AgentReady session context. Context from the two surfaces must not be mixed.
- Inheritance/base-type behavior should only be followed when returned by MCP metadata. Agents must not infer inheritance.
