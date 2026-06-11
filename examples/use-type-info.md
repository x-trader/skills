# Example: Use Type Info

**Endpoint**: start with `/mcp/agent-ready/v1`; use `/mcp` only if full type details are required.

**Skills**: `xtrader-mcp-agent-ready-session`, `xtrader-mcp-agent-ready-catalog`, `xtrader-mcp-type-node-data`, `xtrader-mcp-direct-fallback`

## Sequence

1. Verify active AgentReady session with `get_current_project_context`.
2. Use `search_catalog` or `suggest_nodes_for_intent` to find candidate nodes/types.
3. Use `check_port_compatibility` for source/target port types.
4. If full type schema is required, explain Direct fallback and call `get_type_details` on `/mcp`.
5. For object type creation, verify property names, property types, and required flags before `create_object_type`.
6. For enum type creation, verify exact enum values before `create_enum_type`.
7. Before type update/delete, call `analyze_type_usage` and `analyze_type_impact`.
8. Return to AgentReady and refresh with `get_current_project_context`.

## Key Checks

- [ ] No object properties invented.
- [ ] No enum values invented.
- [ ] Type source identified as project, package, or system.
- [ ] Direct fallback explained before Direct type tools.
- [ ] Usage/impact analysis completed before update/delete.
- [ ] No inheritance assumed unless MCP metadata returns it.
