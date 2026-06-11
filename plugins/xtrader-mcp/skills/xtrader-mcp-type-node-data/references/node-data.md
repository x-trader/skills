# Node Data

Node data includes the configuration needed for a graph node instance.

## Inspect Before Setting

Use AgentReady catalog summaries first. If full schema is needed and AgentReady does not expose it, use Direct fallback with `get_node_details`.

Inspect:

- node source: project, package, or system
- input/output ports
- port direction and type
- required form fields
- optional form fields
- type params
- array port type requirements

## Configure Safely

Use graph-plan operations when possible:

- `setNodeFormData` for form fields
- `setInputPortValue` for literal/default port values
- `setTypeParam` for generic type parameters
- `setArrayPortTypes` for dynamic array port element types

Validate with `validate_graph_plan` before `apply_graph_plan`.

Use Direct fallback only when AgentReady graph plans cannot express the required node data operation.
