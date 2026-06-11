# Direct MCP Risk Matrix

## Safe / Low Risk

| Tool | Guidance |
|---|---|
| `connect_project` | Required first call |
| `get_current_project_context` | Safe refresh |
| `search_packages` | Safe query |
| `list_project_dependencies` | Safe query |
| `get_graph` | Read-only graph fetch |
| `get_graph_summary` | Read-only summary |
| `validate_graph` | Read-only validation |
| `list_backtests` / `get_backtest` / `query_backtest_results` | Read-only backtest queries |
| `list_pending_confirmations` | Read-only query |

## Medium Risk

| Tool | Guidance |
|---|---|
| `add_project_package_dependency` | Audit, explain impact |
| `ensure_package_for_node` | Audit, explain why package is needed |
| `create_object_type` / `create_enum_type` | Validate schema, audit |
| `create_visual_node` | Validate inputs, audit |
| `add_graph_node` / `connect_ports` / `set_node_form_data` | Validate, prefer smaller operations |
| `plan_graph_change` | Validate, inspect plan |
| `create_graph_snapshot` | Required before risky mutations |
| `create_backtest` | Explain parameters, audit |

## High Risk

| Tool | Guidance |
|---|---|
| `remove_project_package_dependency` | Require confirmation, analyze dependency impact first |
| `update_all_dependencies` | Require confirmation, list updates first |
| `delete_type` | Require confirmation, analyze type usage first |
| `delete_visual_node` | Require confirmation |
| `apply_graph_change` | Require validation, snapshot, confirmation |
| `replace_graph` | Require validation, snapshot, confirmation — prefer operation plans |
| `remove_graph_node` | Require confirmation, check connected edges |
| `restore_graph_snapshot` | Require confirmation, explain impact |
| `confirm_action` | Verify pending action details before confirming |
| `cancel_action` | Verify action ID before cancelling |
