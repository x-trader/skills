---
name: xtrader-nodes
description: Use this skill when working with XTrader node schemas, node form data, input port values, generic type params, array port types, .NET runtime node naming, or Direct MCP node-data fallback for AgentReady-first graph workflows.
---

# XTrader Nodes Skill

Load this skill when a task needs full node schema, form data, input values, generic type params, array port types, or .NET runtime node naming guidance.

AgentReady MCP v1 remains the default. Use Direct MCP only when AgentReady lacks the required node capability.

## Core Rules

1. Use AgentReady catalog tools first for node discovery and port compatibility.
2. Never invent node codes, form fields, port types, generic type params, or array element types.
3. Use Direct fallback for full node schema or node data mutation only when AgentReady graph plans cannot express the operation.
4. Before graph apply, validate the graph plan.
5. Set form data, input values, generic params, and array port types only from returned schema/metadata.
6. For Direct node-data writes, load `xtrader-governance` and `xtrader-direct`.
7. If object types, enum types, type compatibility, or type mutation are involved, load `xtrader-types`.

## .NET Runtime Node Knowledge

The entire .NET BCL is available as nodes. Use .NET type names and member patterns to predict node display names during catalog searches.

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

Each assembly is its own package (`System.Runtime`, `System.Collections`, `System.Linq`, etc.). Load [dotnet runtime nodes](references/dotnet-runtime-nodes.md) for the full naming table, excluded types/members, and search guidance.

## Node Data Concepts

- **Node schema**: node identity, source, ports, type params, and form requirements.
- **Form data**: configuration fields for a graph node instance.
- **Input values**: default/literal values for input ports.
- **Type params**: generic bindings for a node instance.
- **Array port types**: dynamic array element type bindings.

## AgentReady-First Workflow

```text
get_current_project_context
-> search_catalog or suggest_nodes_for_intent
-> check_port_compatibility
-> suggest_adapter_nodes if incompatible
-> build graph plan operations using schema-backed values only
-> validate_graph_plan before apply
```

## Direct Fallback Workflow

Use only when AgentReady lacks required node details or node-data mutation capability.

```text
explain missing AgentReady capability
-> load xtrader-direct
-> connect_project on /mcp
-> inspect with get_node_details
-> mutate only if needed and governed
-> validate graph plan or graph impact
-> return to AgentReady context
```

## Primary Tools

AgentReady tools:

- `search_catalog`
- `suggest_nodes_for_intent`
- `check_port_compatibility`
- `suggest_adapter_nodes`
- `validate_graph_plan`
- `apply_graph_plan`

Direct fallback tools:

- `get_node_details`
- `set_node_form_data`
- `set_input_port_value`
- `set_type_param`
- `set_array_port_types`

## References

- Read [node data](references/node-data.md) before setting form data or input values.
- Read [generic type params](references/generic-type-params.md) before binding generic nodes.
- Read [dotnet runtime nodes](references/dotnet-runtime-nodes.md) when searching for .NET BCL nodes.
- Read [Direct node tools](references/direct-node-tools.md) before using Direct MCP node tools.
- Read [anti-patterns](references/anti-patterns.md) when configuring node data.

## Anti-Patterns

- Treating `get_node_details` as AgentReady MCP v1.
- Setting node form data without inspecting required fields.
- Setting input values without type compatibility.
- Setting generic params without schema evidence.
- Setting array port types without validation.
- Connecting ports without checking compatibility.

## Load Next Skill

- **Session**: load `xtrader-session` first if no active session.
- **Catalog**: load `xtrader-catalog` for node discovery and compatibility.
- **Types**: load `xtrader-types` for type details, object/enum types, or type mutation.
- **Visual graphs**: load `xtrader-visual-graphs` for VisualNode, FlowGraph, public port nodes, and port-kind workflows.
- **Graph plan**: load `xtrader-graph-plan` for node data operations in graph plans.
- **Governance**: load `xtrader-governance` before node-data writes.
- **Direct**: load `xtrader-direct` for Direct MCP node tools.
