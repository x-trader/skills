---
name: xtrader-types
description: Use this skill when working with XTrader type details, type compatibility, object types, enum types, JSON-derived types, type usage/impact analysis, or type mutation through AgentReady-first MCP workflows with Direct MCP fallback only when needed.
---

# XTrader Types Skill

Load this skill when a task needs type inspection, type compatibility, object/enum type creation, or type mutation.

AgentReady MCP v1 remains the default. Use Direct MCP only when AgentReady lacks the required type capability.

## Core Rules

1. Use AgentReady catalog tools first for type discovery and port compatibility.
2. Never invent object properties, enum values, type IDs, package names, or inheritance behavior.
3. Use Direct fallback for full type details or type mutation when AgentReady does not expose the needed action.
4. Before type update, rename, move, or delete, inspect usage and impact.
5. Treat project types, package types, and system types differently; package/system types are not project-editable.
6. For Direct writes, load `xtrader-governance` and `xtrader-direct`.
7. If node schema, form data, input values, generic params, or array port types are involved, load `xtrader-nodes`.

## Type Concepts

- **Project types**: user-defined types in the active project version.
- **Package types**: types provided by installed package dependencies.
- **System types**: primitive/system types exposed through MCP metadata.
- **Object types**: structured property collections; verify property names, types, and required flags.
- **Enum types**: named values; inspect exact values before using them.
- **JSON-derived types**: inferred schemas must be reviewed before saving.

## AgentReady-First Workflow

```text
get_current_project_context
-> search_catalog or suggest_nodes_for_intent
-> check_port_compatibility when graph ports are involved
-> use Direct fallback only for missing type details or mutation
```

## Direct Fallback Workflow

Use only when AgentReady lacks required type details or mutation capability.

```text
explain missing AgentReady capability
-> load xtrader-direct
-> connect_project on /mcp
-> inspect with get_type_details or get_type_form_schema
-> analyze usage/impact before mutation
-> mutate only if needed and governed
-> return to AgentReady context
```

## Primary Tools

AgentReady tools:

- `search_catalog`
- `suggest_nodes_for_intent`
- `check_port_compatibility`

Direct fallback tools:

- `search_available_types`
- `get_type_details`
- `get_type_form_schema`
- `check_type_compatibility`
- `suggest_type_for_port`
- `create_object_type`
- `create_enum_type`
- `create_type_from_json_sample`
- `analyze_type_usage`
- `analyze_type_impact`
- `update_type`
- `rename_type`
- `move_type`
- `delete_type`

## References

- Read [type sources](references/type-sources.md) when deciding whether a type is project, package, or system-owned.
- Read [object and enum types](references/object-enum-types.md) before creating or editing object/enum schemas.
- Read [Direct type tools](references/direct-type-tools.md) before using Direct MCP type tools.
- Read [anti-patterns](references/anti-patterns.md) when planning type mutation.

## Anti-Patterns

- Assuming enum values from names alone.
- Creating object schemas without checking available types.
- Treating package/system types as project-editable types.
- Updating/deleting types without usage and impact analysis.
- Assuming inheritance/base-type behavior without MCP metadata.
- Using Direct MCP for type writes without governance.

## Load Next Skill

- **Session**: load `xtrader-session` first if no active session.
- **Catalog**: load `xtrader-catalog` for discovery and compatibility.
- **Nodes**: load `xtrader-nodes` for node schema, form data, input values, generic params, or array port types.
- **Graph plan**: load `xtrader-graph-plan` when selected types are used in graph operations.
- **Governance**: load `xtrader-governance` before type writes.
- **Direct**: load `xtrader-direct` for Direct MCP type tools.
