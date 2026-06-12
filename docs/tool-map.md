# Tool Map

## AgentReady MCP v1 Tools (13 tools — default endpoint)

| Tool | Category | Risk | ReadOnly | Requires Context |
|---|---|---|---|---|
| `open_project_session` | session | Low | No | No |
| `get_current_project_context` | session | Low | Yes | Yes |
| `get_agent_bootstrap_context` | session | Low | No | No |
| `describe_mcp_tooling` | tooling | Low | Yes | No |
| `search_catalog` | catalog | Low | Yes | Yes |
| `resolve_intent_concepts` | catalog | Low | Yes | Yes |
| `suggest_nodes_for_intent` | catalog | Low | Yes | Yes |
| `check_port_compatibility` | catalog | Low | Yes | Yes |
| `suggest_adapter_nodes` | catalog | Low | Yes | Yes |
| `search_graph_patterns` | catalog | Low | Yes | Yes |
| `instantiate_graph_pattern` | catalog | Medium | No | Yes |
| `validate_graph_plan` | graph | Low | Yes | Yes |
| `apply_graph_plan` | graph | High | No | Yes |

## Direct MCP Tool Categories (92 tools — fallback endpoint `/mcp`)

### Project Context (4 tools)

| Tool | Risk |
|---|---|
| `connect_project` | Low |
| `get_current_project_context` | Low |
| `switch_project_version` | Low |
| `describe_project_capabilities` | Low |

### Version (4 tools)

| Tool | Risk |
|---|---|
| `list_project_versions` | Low |
| `create_project_version` | Medium |
| `clone_project_version` | Medium |
| `compare_project_versions` | Low |

### Folder (3 tools)

| Tool | Risk |
|---|---|
| `list_folders` | Low |
| `create_folder` | Low |
| `get_folder_by_path` | Low |

### Package (17 tools)

| Tool | Risk |
|---|---|
| `search_packages` | Low |
| `get_package_details` | Low |
| `list_package_nodes` | Low |
| `list_package_types` | Low |
| `list_project_dependencies` | Low |
| `analyze_dependency_impact` | Low |
| `find_package_for_node` | Low |
| `find_package_for_type` | Low |
| `ensure_package_for_node` | Medium |
| `ensure_package_for_type` | Medium |
| `add_project_package_dependency` | Medium |
| `add_project_reference_dependency` | Medium |
| `update_project_reference_dependency` | Medium |
| `update_project_package_dependency` | Medium |
| `remove_project_package_dependency` | High |
| `get_dependency_updates` | Low |
| `update_all_dependencies` | High |

### Type (15 tools)

| Tool | Risk |
|---|---|
| `get_type_form_schema` | Low |
| `create_type_from_json_sample` | Medium |
| `analyze_type_usage` | Low |
| `analyze_type_impact` | Low |
| `create_object_type` | Medium |
| `create_enum_type` | Medium |
| `list_project_types` | Low |
| `search_available_types` | Low |
| `get_type_details` | Low |
| `check_type_compatibility` | Low |
| `suggest_type_for_port` | Low |
| `update_type` | Medium |
| `rename_type` | Medium |
| `move_type` | Medium |
| `delete_type` | High |

### Node (7 tools)

| Tool | Risk |
|---|---|
| `list_project_visual_nodes` | Low |
| `search_available_nodes` | Low |
| `get_node_details` | Low |
| `create_visual_node` | Medium |
| `rename_visual_node` | Medium |
| `move_visual_node` | Medium |
| `delete_visual_node` | High |

### Graph (16 tools)

| Tool | Risk |
|---|---|
| `get_graph` | Low |
| `get_graph_summary` | Low |
| `validate_graph` | Low |
| `plan_graph_change` | Medium |
| `apply_graph_change` | High |
| `replace_graph` | High |
| `add_graph_node` | Medium |
| `remove_graph_node` | High |
| `connect_ports` | Medium |
| `disconnect_edge` | Medium |
| `set_node_form_data` | Medium |
| `set_input_port_value` | Medium |
| `set_type_param` | Medium |
| `set_array_port_types` | Medium |
| `create_graph_snapshot` | Medium |
| `restore_graph_snapshot` | High |

### Backtest (23 tools)

| Tool | Risk |
|---|---|
| `create_backtest` | Medium |
| `wait_backtest` | Low |
| `search_backtest_logs` | Low |
| `query_backtest_results` | Low |
| `list_backtests` | Low |
| `get_backtest` | Low |
| `get_backtest_overview` | Low |
| `get_backtest_results_summary` | Low |
| `get_backtest_timeline` | Low |
| `get_backtest_snapshot` | Low |
| `get_backtest_issues` | Low |
| `get_backtest_symbol_snapshot` | Low |
| `get_backtest_position_snapshot` | Low |
| `list_trade_sessions` | Low |
| `list_backtest_symbols` | Low |
| `get_backtest_symbol` | Low |
| `list_backtest_logs` | Low |
| `list_backtest_drawings` | Low |
| `list_backtest_positions` | Low |
| `get_backtest_positions_summary` | Low |
| `get_backtest_positions_win_rate` | Low |
| `get_backtest_position` | Low |
| `get_backtest_position_shapes` | Low |

Backtest tools are Direct MCP-only today. Use `xtrader-backtests` and prefer overview/snapshot/issues/summary tools before raw logs, drawings, or full position lists.

### Confirmation (3 tools)

| Tool | Risk |
|---|---|
| `confirm_action` | High |
| `list_pending_confirmations` | Low |
| `cancel_action` | Medium |
