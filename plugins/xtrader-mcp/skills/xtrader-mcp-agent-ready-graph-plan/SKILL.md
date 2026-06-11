---
name: xtrader-mcp-agent-ready-graph-plan
description: Creates, validates, and applies operation-based graph plans through XTrader AgentReady MCP. Guides agents to use instantiate_graph_pattern for known patterns, validate before apply, satisfy governance requirements, and avoid direct graph replacement. Use when creating, editing, repairing, or applying graph changes through AgentReady MCP.
---

# XTrader MCP AgentReady Graph Plan Skill

Load this skill for graph creation, editing, repair, and mutation workflows.

## AgentReady Exposed Tools

- `instantiate_graph_pattern` — create a plan from a known graph pattern (Medium risk)
- `validate_graph_plan` — validate plan preconditions without mutating (Low risk)
- `apply_graph_plan` — apply validated plan (High risk, requires confirmation/snapshot)

## Core Rules

1. Prefer operation-based graph plans over graph replacement.
2. Always validate before apply.
3. Do not use graph replacement as default strategy.
4. Do not connect ports without a compatibility check from catalog skill.
5. Explain changes as operations — add node, connect ports, set value, etc.
6. For risky changes, load governance skill and satisfy snapshot/confirmation requirements.
7. Use `instantiate_graph_pattern` when a known pattern fits the task.

## Operation Vocabulary

When building or describing plans, use these operation types:

- `addGraphNode` — insert a new node instance
- `removeGraphNode` — remove a node and its edges
- `connectPorts` — connect output to input port
- `disconnectEdge` — remove a specific edge
- `setNodeFormData` — configure node form values
- `setInputPortValue` — set default value for an input port
- `setTypeParam` — set generic type parameter
- `setArrayPortTypes` — set dynamic array port types

## Validation Feedback Loop

```text
validate_graph_plan(plan)
-> inspect errors and warnings
-> repair plan (adjust operations, fix ports, add missing nodes)
-> validate_graph_plan again
-> satisfy governance requirements
-> apply_graph_plan
```

## Standard Workflow

```text
get_current_project_context (verify active session)
-> resolve/search catalog if needed
-> instantiate_graph_pattern or build operation plan
-> validate_graph_plan
-> satisfy governance requirements (snapshot, confirmation)
-> apply_graph_plan
```

## Anti-Patterns

- Applying before validation
- Mutating without an active session
- Using `replace_graph` for small changes
- Bypassing governance for high-risk operations
- Ignoring validation warnings
- Connecting ports without checking compatibility

## Load Next Skill

- **Governance**: load `xtrader-mcp-agent-ready-governance` before apply.
- **Catalog**: load `xtrader-mcp-agent-ready-catalog` to find nodes and check ports first.
- **Session**: load `xtrader-mcp-agent-ready-session` first if no active session.
- **Direct fallback**: load `xtrader-mcp-direct-fallback` only if AgentReady graph plan tools are insufficient.
