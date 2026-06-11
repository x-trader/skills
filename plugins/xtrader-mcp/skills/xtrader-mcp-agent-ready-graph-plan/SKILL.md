---
name: xtrader-mcp-agent-ready-graph-plan
description: Use when creating, editing, repairing, validating, explaining, or applying XTrader graph changes through AgentReady MCP graph plans. Guides agents to prefer operation-based plans, validation, snapshots, and governed apply over direct graph replacement.
---

# XTrader MCP AgentReady Graph Plan Skill

Use this skill for graph creation, editing, repair, and mutation workflows.

## Core Rules

1. Prefer operation-based graph plans.
2. Validate before apply.
3. Use dry-run when available.
4. Do not use graph replacement as default strategy.
5. Do not connect ports without compatibility check.
6. Explain changes as operations.
7. For risky changes, require governance, snapshot, or confirmation.

## Primary Tools

- `instantiate_graph_pattern`
- `validate_graph_plan`
- `apply_graph_plan`

Related catalog tools:

- `search_graph_patterns`
- `check_port_compatibility`
- `suggest_adapter_nodes`

## Standard Workflow

```text
get_current_project_context
-> resolve/search catalog if needed
-> instantiate_graph_pattern or build plan
-> validate_graph_plan
-> satisfy governance requirements
-> apply_graph_plan
```

## Anti-Patterns

Do not apply before validation, mutate without active session, bypass governance, replace the graph for small changes, or ignore validation warnings.
