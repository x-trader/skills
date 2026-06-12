# Example: Create Visual Node Public Ports

**Endpoint**: start with `/mcp/agent-ready/v1`; use `/mcp` only if visual-node creation or raw graph access is unavailable through AgentReady.

**Skills**: `xtrader-session`, `xtrader-catalog`, `xtrader-nodes`, `xtrader-visual-graphs`, `xtrader-graph-plan`, `xtrader-governance`, `xtrader-direct`

## Sequence

1. Verify active AgentReady session with `get_current_project_context`.
2. Load `xtrader-visual-graphs` to reason about `VisualNode`, `FlowGraph`, and public port nodes.
3. Use catalog search to resolve official port node codes:
   - `XTrader.Nodes.Core.IO.ValueInputPort`
   - `XTrader.Nodes.Core.IO.ValueOutputPort`
4. If creating the project visual node requires Direct MCP, explain fallback and call `create_visual_node`.
5. Build graph-plan operations to add internal port nodes.
6. Set `InputPortsValues["Name"]` for each public port.
7. Set `TypeParams["T"]` for value/flow ports.
8. Validate the graph plan.
9. Satisfy governance requirements.
10. Apply the graph plan.

## Key Checks

- [ ] Public ports are internal `XTrader.Nodes.Core.IO.*` port nodes.
- [ ] Value/flow public ports have `TypeParams["T"]`.
- [ ] Signal public ports do not require `TypeParams["T"]`.
- [ ] Port names come from `InputPortsValues["Name"]`.
- [ ] The graph is validated before apply.
