# Example: Compose Visual Nodes

**Endpoint**: `/mcp/agent-ready/v1`; use `/mcp` only for missing visual-node or raw graph capabilities.

**Skills**: `xtrader-session`, `xtrader-catalog`, `xtrader-visual-graphs`, `xtrader-nodes`, `xtrader-graph-plan`, `xtrader-governance`

## Sequence

1. Verify active AgentReady session.
2. Find the existing project visual node through catalog/project node search.
3. Inspect its public schema before connecting to it.
4. Add the visual node as a graph node instance in the parent `FlowGraph`.
5. Connect to its generated public ports by exact handle name.
6. Validate and repair the graph plan until valid.
7. Apply only after governance requirements are satisfied.

## Key Checks

- [ ] The nested visual node is found in catalog/project nodes.
- [ ] The graph node `type` uses the visual node's project node code.
- [ ] External ports come from the nested visual node's internal public port nodes.
- [ ] Edges use exact handles from schema.
- [ ] No whole-graph replacement is used for small edits.
