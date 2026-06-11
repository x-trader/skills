---
name: xtrader-mcp-direct-fallback
description: Provides controlled fallback to Direct MCP (/mcp) when XTrader AgentReady MCP v1 lacks the required capability. Covers tool categories, fallback decision rules, context isolation warnings, and return-to-AgentReady workflow. Use only when AgentReady v1 does not expose the required tool.
---

# XTrader MCP Direct Fallback Skill

Load this skill only as a fallback.

- **AgentReady MCP v1** (default): `/mcp/agent-ready/v1`
- **Direct MCP** (fallback): `/mcp`

## When to Use Direct Fallback

| Need | Use Direct MCP? | Reason |
|---|---|---|
| Open/read AgentReady session | No | AgentReady has session tools |
| Search semantic catalog | No | AgentReady has catalog tools |
| Validate/apply AgentReady graph plan | No | AgentReady has governed graph plan tools |
| Backtest creation and analysis | Yes | AgentReady v1 currently lacks these |
| Package/dependency mutation | Yes, carefully | AgentReady v1 lacks package mutation tools |
| Type mutation (create/update/delete) | Yes, carefully | AgentReady v1 lacks type mutation tools |
| Node mutation (create/delete) | Yes, carefully | AgentReady v1 lacks node mutation tools |
| Raw graph read (`get_graph`) | Maybe | AgentReady v1 lacks raw graph read |
| Graph mutation | Avoid if possible | Prefer AgentReady graph plan tools first |
| `replace_graph` / `restore_graph_snapshot` | Only with explicit governance | High risk |

## Direct MCP Tool Categories

| Category | Size | Typical Risk |
|---|---|---|
| Project context | 4 tools | Low |
| Version | 4 tools | Low/Medium |
| Folder | 3 tools | Low |
| Package | 18 tools | Low/Medium/High |
| Type | 16 tools | Low/Medium/High |
| Node | 7 tools | Medium/High |
| Graph | 16 tools | Low/Medium/High |
| Backtest | 23 tools | Low/Medium |
| Confirmation | 3 tools | Low/High |

See `docs/tool-map.md` for the full Direct MCP tool list.

## Core Rules

1. AgentReady MCP v1 is the default. Use Direct MCP only when AgentReady v1 lacks the required capability.
2. Explain to the user why fallback is needed — reference the specific missing capability.
3. Prefer read-only Direct MCP tools when possible.
4. Direct MCP has broader low-level mutation tools — use the smallest tool that accomplishes the task.
5. Direct MCP context is user-scoped, not session-isolated. `get_current_project_context` on Direct MCP differs from the AgentReady version.
6. Connect via `connect_project` when starting a Direct MCP session.
7. For Direct MCP writes, require plan, validation, snapshot, and confirmation when available.
8. Return to AgentReady MCP v1 workflow after the fallback task completes.

## Required Fallback Workflow

```text
AgentReady attempt -> identify missing capability
-> explain fallback reason to user
-> connect_project on /mcp
-> use smallest Direct MCP tool for the task
-> satisfy confirmation/snapshot if needed
-> return to /mcp/agent-ready/v1
-> refresh AgentReady context with get_current_project_context
```

## Direct MCP Context Warning

`get_current_project_context` on Direct MCP is a different implementation from `get_current_project_context` on AgentReady. Do not mix them silently.

## Forbidden / Default-Avoid Cases

- Using Direct MCP because it is easier or has more tools
- Using Direct MCP for graph changes when AgentReady graph plan tools work
- Using `replace_graph` for small edits
- Mixing Direct MCP context with AgentReady session context
- Falling back without explaining why

## Anti-Patterns

- Using Direct MCP as the default endpoint
- Performing direct mutation when AgentReady has graph plan tools
- Ignoring Direct MCP context isolation limitations
- Falling back to Direct MCP for every operation
- Calling Direct MCP deprecated — it is not deprecated, it is not the default

## Load Next Skill

- **Session**: reload `xtrader-mcp-agent-ready-session` after fallback to refresh context.
- **Governance**: load `xtrader-mcp-agent-ready-governance` before Direct MCP writes.
