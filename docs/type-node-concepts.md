# Type and Node Concepts

Use this guide when an agent must reason about XTrader MCP types, node schema, form data, generic params, or array port types.

## Type Sources

| Source | Meaning | Mutation |
|---|---|---|
| Project | Type created in the active project version | Direct MCP only; governed |
| Package | Type supplied by a package dependency | Read-only from project workflows |
| System | Primitive/system type exposed by MCP metadata | Read-only |

## Type Kinds

| Kind | Guidance |
|---|---|
| Object | Verify property names, property types, and required flags |
| Enum | Verify exact value names and values before use |
| Primitive/system | Use only as returned by MCP metadata |
| Generic binding | Bind only from node schema/type param metadata |

Do not assume inheritance/base-type behavior. Follow it only when MCP metadata explicitly returns it.

## .NET Runtime Nodes

Every public .NET BCL type (class, struct, interface, enum) from the SDK reference assemblies is extracted as nodes. Each assembly becomes a package (`System.Runtime`, `System.Collections`, `System.Linq`, etc.). Node display names follow structured naming conventions derived from .NET member names.

See the [dotnet-runtime-nodes reference](plugins/xtrader-mcp/skills/xtrader-nodes/references/dotnet-runtime-nodes.md) for the full naming table, package list, and exclusion rules.

## Node Data

Node data can include:

- node schema
- input/output ports
- port direction and type
- required form data
- optional form data
- input default values
- generic type params
- array port element types
- package/project source

## AgentReady-First Rule

Use AgentReady catalog and compatibility tools first:

- `search_catalog`
- `suggest_nodes_for_intent`
- `check_port_compatibility`
- `suggest_adapter_nodes`

Use Direct MCP only when AgentReady lacks full detail or mutation capability.

## Direct Fallback Examples

Use Direct MCP for:

- `get_node_details` when full node schema is required
- `get_type_details` when full type schema is required
- `create_object_type`, `create_enum_type`, `create_type_from_json_sample` for type creation
- `analyze_type_usage`, `analyze_type_impact` before type update/delete
- `set_node_form_data`, `set_input_port_value`, `set_type_param`, `set_array_port_types` if AgentReady graph plans cannot express the operation
