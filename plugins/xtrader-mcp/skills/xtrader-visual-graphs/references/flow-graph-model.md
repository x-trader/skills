# FlowGraph Model

`FlowGraph` is the persisted visual graph structure used inside `VisualNodeData`.

## Shape

```text
FlowGraph
  nodes: FlowGraph.Node[]
  edges: FlowGraph.Edge[]
  viewport?: { x, y, zoom }
```

## Node

Important fields:

- `id`: graph-local node instance ID. Edges use this value.
- `type`: node code/type, such as a dependency node code or project visual node code.
- `nodeId`: optional catalog/project node database ID.
- `data`: title, form data, type params, array port mappings, input values, execution mode.
- `position`: canvas location.

Graph node IDs are instance IDs, not node codes. Multiple graph nodes can use the same `type` if they are different instances.

## Edge

Important fields:

- `source`: source graph node ID.
- `sourceHandle`: output port handle on source.
- `target`: target graph node ID.
- `targetHandle`: input port handle on target.
- `id`: edge ID.

Handle names are schema port names. Dotted handles address member ports, such as `Slot.Name`.

## Agent Rules

- Never invent node `type`; resolve it through catalog or node details.
- Never invent port handles; inspect schema or validation output.
- Prefer operation-based graph plans over whole graph replacement.
- Preserve existing graph node IDs and edge IDs unless the task requires a change.
