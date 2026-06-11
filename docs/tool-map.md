# Tool Map

## AgentReady MCP v1 Tools (Default)

| Tool                          | Category        | Description                             |
|-------------------------------|-----------------|-----------------------------------------|
| `open_project_session`        | Session         | Open isolated project session           |
| `get_agent_bootstrap_context` | Session         | Read bootstrap context                  |
| `get_current_project_context` | Session         | Refresh session context                 |
| `describe_mcp_tooling`        | Governance      | Inspect tool manifest, risk, metadata   |
| `search_catalog`              | Catalog         | Search semantic catalog                 |
| `resolve_intent_concepts`     | Catalog         | Map intent to semantic concepts         |
| `suggest_nodes_for_intent`    | Catalog         | Suggest nodes matching intent           |
| `check_port_compatibility`    | Catalog         | Check port type/direction compatibility |
| `suggest_adapter_nodes`       | Catalog         | Suggest adapter nodes for mismatched ports |
| `search_graph_patterns`       | Catalog/Graph   | Search composable graph patterns        |
| `instantiate_graph_pattern`   | Graph           | Create graph plan from pattern          |
| `validate_graph_plan`         | Graph           | Validate graph plan                     |
| `apply_graph_plan`            | Graph           | Apply validated graph plan              |

## Direct MCP Tool Categories (Fallback)

| Category              | Description                                   |
|-----------------------|-----------------------------------------------|
| Project               | Connect, configure, version info              |
| Package               | Install, remove, dependency management        |
| Node                  | Create, update, delete, inspect               |
| Graph                 | Read, replace, snapshot restore               |
| Backtest              | Run backtests, fetch results                  |
| Confirmation          | Confirm destructive operations                |
| Snapshot              | Create, restore, list snapshots               |
| Execution             | Run live/protected execution (if available)   |
