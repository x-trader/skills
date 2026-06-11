---
name: xtrader-mcp-agent-ready-governance
description: Enforces XTrader AgentReady governance rules by reading the tool manifest, respecting project mode, risk levels, confirmation, and snapshot requirements before write or risky operations. Use before graph-plan apply, dependency mutation, snapshot restore, destructive changes, or live/protected execution.
---

# XTrader MCP AgentReady Governance Skill

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
| Policy requires snapshot | Call `create_graph_snapshot` before mutation |
| Policy requires confirmation | Present changes, wait for `confirm_action` |

## Core Rules

1. Call `describe_mcp_tooling` before initiating any write workflow.
2. Respect tool `readOnly` and `destructive` metadata from the manifest.
3. Respect project mode — Design allows more freedom than LiveProtected.
4. Require `validate_graph_plan` before `apply_graph_plan`.
5. Require confirmation for destructive, live, or protected changes.
6. Never silently apply high-risk changes.
7. Prefer AgentReady governed tools over Direct MCP direct mutation.

## Standard Workflow

```text
describe_mcp_tooling
-> classify operation risk from manifest
-> check project mode (Design / LiveProtected)
-> validate plan if graph-related
-> create snapshot if policy requires
-> require confirmation if policy requires
-> apply only if all governance checks pass
-> summarize governance result
```

## Anti-Patterns

- Treating observe-mode governance as permission to be careless
- Bypassing validation because the change seems small
- Using Direct MCP write tools when AgentReady governed tools exist
- Hiding risk from the user
- Silently applying high-risk changes

## Load Next Skill

- **Session**: load `xtrader-mcp-agent-ready-session` first if no active session.
- **Graph plan**: load `xtrader-mcp-agent-ready-graph-plan` for plan creation and validation.
- **Direct fallback**: load `xtrader-mcp-direct-fallback` only when AgentReady v1 lacks the required capability.
