---
name: xtrader-governance
description: Use this skill before XTrader write or risky operations, including graph-plan apply, dependency mutation, type/node mutation, snapshot restore, destructive changes, or live/protected execution. Enforces project mode, risk levels, confirmation, snapshot, and validation requirements.
---

# XTrader Governance Skill

Load this skill before any write or risky operation.

## Tool Manifest Fields

`describe_mcp_tooling` returns per-tool metadata:

| Field | Meaning |
|---|---|
| `category` | Tool group: session, catalog, graph, tooling |
| `risk` | Low, Medium, High, Critical |
| `readOnly` | True if the tool does not mutate state |
| `destructive` | True if the tool can cause irreversible changes |
| `requiresContext` | True if an active session is required |
| `requiresValidation` | True if plan validation is required before use |
| `requiresPlan` | True if a plan must be created first |
| `requiresConfirmation` | True if user confirmation is required |
| `requiresSnapshot` | True if a graph snapshot must exist before mutation |
| `preconditions` | Array of conditions that must be met |
| `recommendedBefore` | Tools that should be called before this one |
| `recommendedAfter` | Tools that should be called after this one |
| `commonMistakes` | Array of known agent errors to avoid |

## Decision Matrix

| Condition | Action |
|---|---|
| Tool is `readOnly` | Allow after verifying active session |
| Medium write in `Design` mode | Validate and audit |
| Medium write in `LiveProtected` mode | Require confirmation |
| High risk (graph mutation, delete, replace) | Require plan, snapshot, confirmation |
| Tool is `destructive` | Require confirmation, notify user of impact |
| Critical risk | Deny unless admin or explicit live-protected policy permits |
| Policy requires snapshot | Create or reference a snapshot through the available workflow; use Direct fallback only if AgentReady lacks the needed action |
| Policy requires confirmation | Present changes and obtain explicit confirmation; use Direct fallback only if an MCP confirmation tool is required |

## Core Rules

1. Call `describe_mcp_tooling` before initiating any write workflow.
2. Respect tool `readOnly` and `destructive` metadata from the manifest.
3. Respect project mode — Design allows more freedom than LiveProtected.
4. Require `validate_graph_plan` before `apply_graph_plan`.
5. Require confirmation for destructive, live, or protected changes.
6. If snapshot or confirmation requires a Direct-only tool, load Direct fallback and explain why.
7. Never silently apply high-risk changes.
8. Prefer AgentReady governed tools over Direct MCP direct mutation.
9. Treat type update/delete, node deletion, node data mutation, and generic/array port mutation as governance-sensitive.
10. Treat backtest result reads as generally read-only; treat `create_backtest` as a Direct MCP action that must be explained and bounded.

## Standard Workflow

```text
describe_mcp_tooling
-> classify operation risk from manifest
-> check project mode (Design / LiveProtected)
-> validate plan if graph-related
-> satisfy snapshot requirement if policy requires
-> obtain confirmation if policy requires
-> use Direct fallback only for missing snapshot/confirmation tooling
-> apply only if all governance checks pass
-> summarize governance result
```

## Anti-Patterns

- Treating observe-mode governance as permission to be careless
- Bypassing validation because the change seems small
- Using Direct MCP write tools when AgentReady governed tools exist
- Hiding risk from the user
- Silently applying high-risk changes
- Updating/deleting types without usage and impact analysis
- Mutating node data or generic params without validation
- Mutating project graph/type/package state during backtest result inspection

## Load Next Skill

- **Session**: load `xtrader-session` first if no active session.
- **Graph plan**: load `xtrader-graph-plan` for plan creation and validation.
- **Types**: load `xtrader-types` before type mutation.
- **Nodes**: load `xtrader-nodes` before node data mutation, generic params, or array port changes.
- **Backtests**: load `xtrader-backtests` for backtest execution or result inspection.
- **Direct**: load `xtrader-direct` only when AgentReady v1 lacks the required capability.
