---
name: xtrader-mcp-agent-ready-governance
description: Use before risky, destructive, write, graph-plan apply, package-changing, snapshot-changing, live/protected, or confirmation-required XTrader MCP operations. Guides agents to read tool manifest risk metadata, respect project mode, validate plans, require snapshots/confirmation, and avoid unsafe direct mutation.
---

# XTrader MCP AgentReady Governance Skill

Use this skill before any write or risky operation.

## Core Rules

1. Read `describe_mcp_tooling` before write workflows.
2. Respect tool `ReadOnly` and `Destructive` metadata.
3. Respect project mode and risk policy.
4. Require validation before graph apply.
5. Require snapshot for risky graph changes when policy says so.
6. Require confirmation for destructive/live/protected changes.
7. Never silently apply high-risk changes.
8. Prefer AgentReady governed tools over legacy direct mutation.

## Risk Examples

High-risk operations include graph replacement, node removal, package dependency mutation, snapshot restore, live/protected execution, and destructive apply.

## Standard Workflow

```text
describe_mcp_tooling
-> classify operation risk
-> check project mode
-> validate plan if graph-related
-> require snapshot/confirmation if needed
-> apply only if allowed
-> summarize governance result
```

## Anti-Patterns

Do not treat observe-mode governance as permission to be careless, bypass validation, use legacy write tools when AgentReady governed tools exist, or hide risk from the user.
