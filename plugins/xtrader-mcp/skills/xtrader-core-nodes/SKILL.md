---
name: xtrader-core-nodes
description: Guides agents through XTrader Core nodes — the building blocks of visual graphs. Covers arithmetic, logic, flow control, data manipulation, IO port infrastructure, and events. Use when building, explaining, or planning graphs that use core visual scripting nodes.
---

# XTrader Core Nodes Skill

Load this skill when a task involves building, explaining, or planning graphs that use Core nodes — the building blocks of XTrader Visual Scripting.

Core nodes are defined in `XTrader.Nodes.Core` and are separate from .NET BCL runtime nodes. They have their own source-generated catalog via `[Node]` and `[Port]` attributes.

## Core Rules

1. Search for Core nodes by their `[Node("DisplayName")]` attribute name in catalog, not by .NET type name patterns.
2. Never invent node names, port names, or port directions — always use MCP catalog or node detail results.
3. Core nodes are in the `XTrader.Nodes.Core` package. They are excluded from .NET BCL extraction.
4. For form data, input values, type params, and array port types, load `xtrader-nodes`.
5. For VisualNode composition and public ports, load `xtrader-visual-graphs`.
6. Before graph apply, validate the graph plan.

## Node Categories

| Category | Nodes | Key Use |
|---|---|---|
| IO / Port | `ValueInputPortNode`, `ValueOutputPortNode`, `SignalInputPortNode`, `SignalOutputPortNode`, `FlowInputPortNode`, `FlowOutputPortNode` | Graph boundary, public ports |
| Math | `AdditionNode<T>`, `SubtractionNode<T>`, `MultiplicationNode<T>`, `DivisionNode<T>` | Numeric arithmetic |
| Logic | `AndNode`, `OrNode`, `NotNode`, `TernaryConditionNode<T>` | Boolean logic |
| Comparison | `EqualNode<T>`, `NotEqualNode<T>`, `GreaterNode<T>`, `LessNode<T>`, `GreaterOrEqualNode<T>`, `LessOrEqualNode<T>` | Value comparison |
| Flow Control | `SequenceNode`, `SwitchNode<T>`, `DoOnceNode`, `FlipFlopNode`, `GateNode`, `IfNode`, `IfNullNode<T>` | Branching, gating |
| Loops | `ForEachNode<T>`, `ForLoopNode`, `WhileLoopNode` | Iteration |
| Type Conversion | `ToFlowNode<T>`, `FromFlowNode<T>`, `CastNode<TIn, TOut>` | Value ↔ flow, casting |
| Exceptions | `TryCatchNode`, `ThrowNode`, `ThrowIfNullNode<T>` | Error handling |
| Timing | `DelayNode` | Async delay |
| Async | `AsyncExecutorNode<T>` | Execute Task\<T\> |
| Variables | `VariableNode<T>`, `PredicateNode<T>`, `FuncNode<TSource, TResult>` | Stateful values, delegates |
| Collections | `BufferNode<T>` | Buffer values into lists |
| Objects | `MapperNode`, `SelectNode`, `SetPropertyNode` | Object construction, projection, mutation |
| Null Utilities | `NullCheckNode<T>`, `NullValueNode<T>`, `NullCoalesceNode<T>`, `NullForgivingNode<T>` | Null handling |
| Events | `OnStartNode` | Graph startup entry point |

## AgentReady-First Workflow

```text
search_catalog or suggest_nodes_for_intent
-> check port compatibility with check_port_compatibility
-> suggest_adapter_nodes if incompatible
-> build graph plan operations
-> validate_graph_plan before apply
```

Search Core nodes by display name (e.g., `If`, `ForEach`, `Addition`, `Variable`). Generic nodes appear with type params bound (e.g., `Addition Int32`, `ForEach String`).

## Load References

- Read [core-nodes-reference](references/core-nodes-reference.md) for the full node catalog, descriptions, and base class hierarchy.

## Load Next Skill

- **Session**: load `xtrader-session` first if no active session.
- **Catalog**: load `xtrader-catalog` for discovery and compatibility.
- **Types**: load `xtrader-types` for type details, object/enum types, or type mutation.
- **Nodes**: load `xtrader-nodes` for node schema, form data, input values, type params, and array port types.
- **Visual graphs**: load `xtrader-visual-graphs` for VisualNode, FlowGraph, public ports, and port kinds.
- **Graph plan**: load `xtrader-graph-plan` for graph plan operations.
- **Governance**: load `xtrader-governance` before node writes.
- **Direct**: load `xtrader-direct` for Direct MCP node tools.
