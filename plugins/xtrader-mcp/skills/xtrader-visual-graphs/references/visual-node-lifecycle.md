# VisualNode Lifecycle

A `VisualNode` is a project node/script backed by an internal `FlowGraph`.

## Creation

Direct MCP exposes `create_visual_node` for project visual node creation when AgentReady lacks that capability. Creation initializes an empty graph so compilation does not fail.

After creation, graph edits add internal nodes, public port nodes, and edges.

## Save / Update

When a visual node graph is saved:

1. The graph is stored as `VisualNodeData(FlowGraph Graph)`.
2. XTrader scans internal official port nodes.
3. It syncs those port nodes into the visual node's external `NodeSchema`.
4. Compilation verifies the project version.

## Reuse

Once created, a visual node is available as a project node. It can be added inside another visual node graph by using its project node code as the graph node `type`.

This is how a node can be used inside another node and called from another graph.

## Agent Rules

- Use catalog/project node search to find visual nodes before adding them to another graph.
- Treat visual-node deletion as risky because other graphs may reference it.
- Treat graph update as a write requiring validation and governance.
- Do not manually edit the external schema; expose ports using internal port nodes.
