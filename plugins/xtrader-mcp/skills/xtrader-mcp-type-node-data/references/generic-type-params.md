# Generic Type Params and Array Port Types

Generic type params bind a node instance to concrete types. Array port types bind dynamic array ports to element types.

## Rules

- Do not guess generic parameter names.
- Do not bind generic params from natural language alone.
- Inspect returned node schema or Direct `get_node_details` output when needed.
- Match generic params across connected ports when compatibility requires it.
- Use `check_port_compatibility` before planning connections.
- Validate after setting type params or array port types.

## Operations

Use graph-plan operations when supported:

- `setTypeParam`
- `setArrayPortTypes`

Use Direct fallback only when required:

- `set_type_param`
- `set_array_port_types`

If validation reports generic mismatch, adjust the type param bindings and validate again.
