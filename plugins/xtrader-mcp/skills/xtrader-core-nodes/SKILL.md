---
name: xtrader-core-nodes
description: Guides agents through XTrader Core node capabilities for visual graphs. Covers arithmetic, logic, flow control, data manipulation, IO port nodes, and events. Use when building, explaining, or planning graphs that use Core visual scripting nodes.
---

# XTrader Core Nodes Skill

Load this skill when a task involves building, explaining, or planning graphs that use Core nodes, the building blocks of XTrader Visual Scripting.

Core nodes are available through the MCP catalog from the `XTrader.Nodes.Core` package. They are separate from .NET runtime nodes and do not use .NET runtime naming patterns like `Create {TypeName}` or `{MethodName} {TypeName}`.

## Core Rules

1. Search for Core nodes by catalog display names, not by .NET runtime node naming patterns.
2. Never invent node names, port names, or port directions; always use MCP catalog or node detail results.
3. Core nodes are in the `XTrader.Nodes.Core` package. Treat them as first-class visual scripting nodes, not .NET runtime type/member nodes.
4. For form data, input values, type params, and array port types, load `xtrader-nodes`.
5. For VisualNode composition and public ports, load `xtrader-visual-graphs`.
6. Before graph apply, validate the graph plan.

## Node Categories

| Category | Nodes | Key Use |
|---|---|---|
| IO / Port | `ValueInputPort`, `ValueOutputPort`, `SignalInputPort`, `SignalOutputPort`, `FlowInputPort`, `FlowOutputPort` | Graph boundary, public ports |
| Math | `Addition`, `Subtraction`, `Multiplication`, `Division` | Numeric arithmetic |
| Logic | `And`, `Or`, `Not`, `TernaryCondition` | Boolean logic |
| Comparison | `Equal`, `NotEqual`, `Greater`, `Less`, `GreaterOrEqual`, `LessOrEqual` | Value comparison |
| Flow Control | `Sequence`, `Switch`, `DoOnce`, `FlipFlop`, `Gate`, `If`, `IfNull` | Branching, gating |
| Loops | `ForEach`, `ForLoop`, `WhileLoop` | Iteration |
| Type Conversion | `ToFlow`, `FromFlow`, `Cast` | Value to flow, flow to value, casting |
| Exceptions | `TryCatch`, `Throw`, `ThrowIfNull` | Error handling |
| Timing | `Delay` | Async delay |
| Async | `AsyncExecutor` | Execute asynchronous result-producing work |
| Variables | `Variable`, `Predicate`, `Func` | Stateful values and reusable predicates/functions |
| Collections | `Buffer` | Buffer values into lists |
| Objects | `Mapper`, `Select`, `SetProperty` | Object construction, projection, mutation |
| Null Utilities | `NullCheck`, `NullValue`, `NullCoalesce`, `NullForgiving` | Null handling |
| Events | `Start` | Graph startup entry point |

## AgentReady-First Workflow

```text
search_catalog or suggest_nodes_for_intent
-> check port compatibility with check_port_compatibility
-> suggest_adapter_nodes if incompatible
-> build graph plan operations
-> validate_graph_plan before apply
```

Search Core nodes by display name (e.g., `If`, `ForEach`, `Addition`, `Variable`). Typed nodes may appear with concrete type bindings in catalog results, such as `Addition Int32` or `ForEach String`.

## Load References

- Read [core-nodes-reference](references/core-nodes-reference.md) for the full agent-facing node catalog and search guidance.

## Load Next Skill

- **Session**: load `xtrader-session` first if no active session.
- **Catalog**: load `xtrader-catalog` for discovery and compatibility.
- **Types**: load `xtrader-types` for type details, object/enum types, or type mutation.
- **Nodes**: load `xtrader-nodes` for node schema, form data, input values, type params, and array port types.
- **Visual graphs**: load `xtrader-visual-graphs` for VisualNode, FlowGraph, public ports, and port kinds.
- **Graph plan**: load `xtrader-graph-plan` for graph plan operations.
- **Governance**: load `xtrader-governance` before node writes.
- **Direct**: load `xtrader-direct` for Direct MCP node tools.
