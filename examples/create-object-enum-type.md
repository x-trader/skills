# Example: Create Object or Enum Type

**Endpoint**: `/mcp` through Direct fallback, because type creation is Direct MCP only.

**Skills**: `xtrader-session`, `xtrader-types`, `xtrader-governance`, `xtrader-direct`

## Object Type Sequence

1. Start from AgentReady session context.
2. Explain Direct fallback because AgentReady v1 does not expose type creation.
3. Call `connect_project` on Direct MCP.
4. Use `search_available_types` to verify referenced property types exist.
5. Call `create_object_type` with explicit properties.
6. Return to AgentReady and refresh context.

## Enum Type Sequence

1. Start from AgentReady session context.
2. Explain Direct fallback because AgentReady v1 does not expose enum creation.
3. Call `connect_project` on Direct MCP.
4. Confirm exact enum value names and values with the user or MCP metadata.
5. Call `create_enum_type`.
6. Return to AgentReady and refresh context.

## Key Checks

- [ ] Direct fallback reason explained.
- [ ] Referenced property types verified.
- [ ] Enum values explicitly known.
- [ ] Governance loaded for risky changes.
- [ ] Returned to AgentReady after Direct mutation.
