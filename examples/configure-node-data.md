# Example: Configure Node Data

**Endpoint**: start with `/mcp/agent-ready/v1`; use `/mcp` only if full node schema or Direct node-data mutation is required.

**Skills**: `xtrader-session`, `xtrader-catalog`, `xtrader-nodes`, `xtrader-graph-plan`, `xtrader-governance`, `xtrader-direct`

## Sequence

1. Verify active AgentReady session with `get_current_project_context`.
2. Use catalog tools to select the node and check port compatibility.
3. If full schema is required, explain Direct fallback and call `get_node_details` on `/mcp`.
4. Inspect required form fields, input ports, type params, and array port requirements.
5. Build graph-plan operations when supported:
   - `setNodeFormData`
   - `setInputPortValue`
   - `setTypeParam`
   - `setArrayPortTypes`
6. Call `validate_graph_plan`.
7. Fix validation errors and validate again.
8. Satisfy governance requirements.
9. Call `apply_graph_plan`.

## Direct Fallback Variant

If AgentReady graph plans cannot express the operation, use Direct MCP with explanation:

```text
connect_project
-> get_node_details
-> set_node_form_data or set_type_param or set_array_port_types
-> validate_graph
-> return to AgentReady
```

## Key Checks

- [ ] Form fields come from schema, not guesses.
- [ ] Input values match expected port types.
- [ ] Generic params come from node schema.
- [ ] Array port element types are validated.
- [ ] Graph plan validated before apply.
- [ ] Direct MCP used only when AgentReady lacks the capability.
