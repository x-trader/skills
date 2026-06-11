---
name: xtrader-mcp-type-node-data
description: Guides agents through XTrader MCP type, node schema, node data, generic type parameter, array port, object type, and enum type workflows. Use when inspecting or configuring type info, node form data, input values, generic params, array port types, or when Direct MCP fallback is needed for full type/node details or mutation.
---

# XTrader MCP Type and Node Data Skill

Load this skill when a task needs type details, node schema, node data configuration, generic type params, array port types, object types, or enum types.

AgentReady MCP v1 remains the default. Use Direct MCP only when AgentReady lacks the required type/node capability.

## Core Rules

1. Use AgentReady catalog tools first for node/type discovery and port compatibility.
2. Never invent object properties, enum values, node form fields, port types, generic type params, or array element types.
3. Use Direct fallback for full node schema, full type details, type mutation, node data mutation, or generic/array port mutation when AgentReady does not expose the needed action.
4. Before type update/delete, inspect usage and impact.
5. Before graph apply, validate the graph plan.
6. Do not infer inheritance/base-type behavior unless MCP metadata explicitly returns it.
7. For Direct writes, load governance and direct-fallback skills.

## .NET Runtime Node Knowledge

The entire .NET BCL is available as nodes. Agents should use knowledge of .NET type names and member patterns to predict node display names during catalog searches.

| Member | Display Pattern | Example |
|---|---|---|
| Constructor | `Create {TypeName}` | `Create List<T>` |
| Method | `{MethodName} {TypeName}` | `Add List<T>`, `Parse Int32` |
| Property getter | `Get {PropertyName} of {TypeName}` | `Get Count of List<T>` |
| Property setter | `Set {PropertyName} of {TypeName}` | `Set Capacity of List<T>` |
| Enum constant | `{TypeName}.{MemberName}` | `DayOfWeek.Sunday` |
| Enum parse | `Parse {TypeName}` / `Try Parse {TypeName}` | `Parse DayOfWeek` |
| Flags compose | `Compose {TypeName} Flags` | `Compose BindingFlags Flags` |
| Flags split | `Split {TypeName} Flags` | `Split BindingFlags Flags` |

Each assembly is its own package (`System.Runtime`, `System.Collections`, `System.Linq`, etc.). Load the [dotnet-runtime-nodes](references/dotnet-runtime-nodes.md) reference for the full naming table, excluded types/members, and search guidance.

## AgentReady-First Workflow

```text
get_current_project_context
-> search_catalog or suggest_nodes_for_intent
-> check_port_compatibility
-> suggest_adapter_nodes if incompatible
-> validate_graph_plan before apply
```

## Direct Fallback Workflow

Use only when AgentReady lacks required details or mutation capability.

```text
explain missing AgentReady capability
-> connect_project on /mcp
-> inspect with get_node_details or get_type_details
-> mutate only if needed and governed
-> validate graph/type impact
-> return to AgentReady context
```

## Type Concepts

- **Project types**: user-defined types in the active project version.
- **Package types**: types provided by installed package dependencies.
- **System types**: primitive/system types exposed through MCP metadata.
- **Object types**: structured property collections; verify property names, types, and required flags.
- **Enum types**: named values; inspect values before using them.
- **Generic usage**: bind node type params only from returned schema/metadata.

## Node Data Concepts

- **Node schema**: node identity, source, ports, type params, and form requirements.
- **Form data**: configuration fields for a graph node instance.
- **Input values**: default/literal values for input ports.
- **Type params**: generic bindings for a node instance.
- **Array port types**: dynamic array element type bindings.

## Primary Tools

AgentReady tools:

- `search_catalog`
- `suggest_nodes_for_intent`
- `check_port_compatibility`
- `suggest_adapter_nodes`
- `validate_graph_plan`
- `apply_graph_plan`

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
- `get_node_details`
- `set_node_form_data`
- `set_input_port_value`
- `set_type_param`
- `set_array_port_types`

## Anti-Patterns

- Assuming enum values from names alone
- Creating object schemas without checking available types
- Treating `get_node_details` as AgentReady MCP v1
- Setting type params without validation
- Updating/deleting types without usage and impact analysis
- Assuming inheritance exists without MCP metadata

## Load Next Skill

- **Catalog**: load `xtrader-mcp-agent-ready-catalog` for discovery and compatibility.
- **Graph plan**: load `xtrader-mcp-agent-ready-graph-plan` for node data operations in graph plans.
- **Governance**: load `xtrader-mcp-agent-ready-governance` before type/node writes.
- **Direct fallback**: load `xtrader-mcp-direct-fallback` for Direct MCP type/node tools.
