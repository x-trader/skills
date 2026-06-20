---
name: xtrader-visual-graphs
description: Use this skill when creating, explaining, editing, or composing XTrader VisualNodes and FlowGraphs through MCP. Covers VisualNode as a reusable graph-backed node, graph nodes and edges, value/signal/flow/array/group port kinds, public port nodes, dynamic ArrayPorts, dotted handles, nested visual nodes, and validation rules.
---

# XTrader Visual Graphs Skill

Load this skill when a task involves VisualNode structure, FlowGraph shape, nested visual-node composition, public port exposure, or port-kind reasoning.

This skill is MCP-only. Do not use it as guidance for writing custom C# runtime node classes; use it to operate through XTrader MCP catalog, node detail, graph plan, validation, and controlled Direct fallback workflows.

## Core Model

1. A `VisualNode` is a project-created node/script whose implementation is an internal `FlowGraph`.
2. The internal graph is stored as `VisualNodeData(FlowGraph Graph)`.
3. A visual node compiles into a reusable runtime node class and can be added inside another visual node graph like any other available node.
4. A `FlowGraph` contains `nodes`, `edges`, and optional `viewport`.
5. A graph node has `id`, `type`, optional `nodeId`, `data`, and optional position metadata.
6. A graph edge connects `source.sourceHandle` to `target.targetHandle`.
7. Public ports of a visual node are derived from special internal port nodes in `XTrader.Nodes.Core.IO`.

## Port Kinds

| Kind | Meaning | Common handle shape |
|---|---|---|
| `value` | One typed data value. | `Output`, `Input` |
| `signal` | Control-only trigger with no payload. | `Then`, `In` |
| `flow` | Trigger plus typed payload. | `Then`, `In`, domain-specific flow names |
| `array` | Dynamic collection-style port with configured element/member types. | `Items`, `ArrayPort.Item` |
| `group` | Named set of typed value members. | `Slot.Name`, `Slot.Age` |

Read [port kinds](references/port-kinds.md) when choosing or validating connections.

## Public Port Nodes

To expose a public port on a visual node, add one of these internal port nodes to its graph:

- `XTrader.Nodes.Core.IO.ValueInputPort`
- `XTrader.Nodes.Core.IO.ValueOutputPort`
- `XTrader.Nodes.Core.IO.SignalInputPort`
- `XTrader.Nodes.Core.IO.SignalOutputPort`
- `XTrader.Nodes.Core.IO.FlowInputPort`
- `XTrader.Nodes.Core.IO.FlowOutputPort`

Port-node rules:

1. `InputPortsValues["Name"]` defines the external public port name.
2. `InputPortsValues["Description"]` is optional.
3. Value and flow port nodes require `TypeParams["T"]`.
4. Signal port nodes do not carry a value type.
5. Only official `XTrader.Nodes.Core.IO.*` port nodes count as visual-node public port nodes.
6. Do not invent external schema ports manually; make them through graph port nodes and validation.

Read [port node patterns](references/port-node-patterns.md) before exposing public ports.

## Graph Node Data

Use graph node `data` fields only with schema evidence:

- `Title`: display title.
- `FormData`: node-specific configuration object.
- `TypeParams`: generic type bindings, such as `T`, `TInput`, or `TOutput`.
- `ArrayPorts`: dynamic type definitions for array/group-style ports.
- `InputPortsValues`: literal/default input values.
- `ExecutionMode`: flowable or pure when supported.

Load `xtrader-nodes` before setting form data, input values, type params, or array port types.

## Dynamic Array And Group Ports

Array/group ports are schema-level concepts. Current public visual-node port nodes cover value/signal/flow; there are no dedicated public `GroupInputPort` or `GroupOutputPort` nodes yet.

- `ArrayPortSchema` represents a dynamic array-like port.
- `GroupPortSchema` represents named typed members.
- `FlowGraph.Node.Data.ArrayPorts` supplies dynamic member types for array and group ports.
- Dotted handles address members, such as `Slot.Name`, `Slot.Age`, or `ArrayPort.Item`.
- `MapperNode` is the concrete group-port example.
- `SelectNode` uses normal value ports, not array ports.

Read [dynamic array and group ports](references/dynamic-array-group-ports.md) before configuring `ArrayPorts` or dotted handles.

## MCP Workflow

```text
xtrader-session
-> xtrader-catalog to find available project/dependency nodes
-> xtrader-types if object/enum/compatibility details are needed
-> xtrader-nodes if schema, form data, input values, type params, or ArrayPorts are needed
-> xtrader-visual-graphs to reason about graph shape, public ports, and composition
-> xtrader-graph-plan to build and validate operations
-> xtrader-governance before apply or risky changes
```

Use Direct MCP only when AgentReady v1 lacks the required visual-node creation, raw graph read, node detail, or low-level mutation capability. Load `xtrader-direct` before Direct fallback.

## Validation Rules

Before apply, validate that:

- every graph node `type` exists in catalog/node details;
- every edge source handle exists on source output ports;
- every edge target handle exists on target input ports;
- port kinds match (`value` to `value`, `signal` to `signal`, etc.);
- value/flow/array/group member types are compatible;
- required user-provided type params are set;
- required form data fields are present;
- `ArrayPorts` only target existing `ArrayPortSchema` or `GroupPortSchema` ports;
- visual-node public ports are represented by official `XTrader.Nodes.Core.IO.*` port nodes.

Read [validation](references/validation.md) when repairing graph errors.

## Anti-Patterns

- Assuming `SelectNode` has array ports; it has value input/output ports.
- Inventing visual-node public ports outside the internal port-node pattern.
- Using non-`XTrader.Nodes.Core.IO` port node types for public ports.
- Connecting `array` to `value` or `signal` to `flow` without schema support.
- Using dotted handles without checking whether the root port is group/array-compatible.
- Setting `TypeParams`, `FormData`, `InputPortsValues`, or `ArrayPorts` from guesses.
- Replacing whole graphs when operation-based graph plans can express the change.

## Load Next Skill

- **Session**: load `xtrader-session` first if no active session.
- **Catalog**: load `xtrader-catalog` to find project/dependency nodes and patterns.
- **Types**: load `xtrader-types` for object/enum types and compatibility.
- **Core nodes**: load `xtrader-core-nodes` when working with Core visual scripting nodes (arithmetic, logic, flow control, data manipulation, IO ports).
- **Nodes**: load `xtrader-nodes` for node schema, form data, input values, type params, and array port types.
- **Graph plan**: load `xtrader-graph-plan` to create, validate, and apply graph changes.
- **Governance**: load `xtrader-governance` before writes or risky changes.
- **Direct**: load `xtrader-direct` only when AgentReady v1 lacks the required capability.
