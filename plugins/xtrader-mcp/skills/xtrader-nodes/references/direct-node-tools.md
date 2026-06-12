# Direct Node Tools

Use Direct MCP only when AgentReady v1 lacks the required node schema or node-data mutation capability.

## Read / Inspect

| Tool | Use |
|---|---|
| `get_node_details` | Inspect node schema, ports, type params, and form requirements |

## Mutate

| Tool | Risk guidance |
|---|---|
| `set_node_form_data` | Validate fields against node schema, then validate graph |
| `set_input_port_value` | Validate expected port type and literal value |
| `set_type_param` | Bind only schema-returned generic parameter names |
| `set_array_port_types` | Validate array element types and downstream compatibility |
