---
name: xtrader-session
description: Use this skill when connecting to XTrader AgentReady MCP for the first time, selecting a project/version, refreshing session context, reading bootstrap capabilities, or preparing catalog, graph, governance, type, node, backtest, or Direct fallback workflows.
---

# XTrader Session Skill

Load this skill before any AgentReady MCP workflow.

Default endpoint: `/mcp/agent-ready/v1`

## Core Rules

1. Call `open_project_session` or `get_agent_bootstrap_context` first — never call catalog, graph, or governance tools without an active session.
2. Extract from bootstrap output: project name, version, mode (Design/LiveProtected), capabilities, risk policy, and resource links.
3. Use `get_current_project_context` to refresh session state, not to bootstrap.
4. Preserve session identity (session ID, project context) across all follow-up calls in the same conversation.
5. Do not silently mix Direct MCP (`/mcp`) context with AgentReady session context — the two surfaces return different context scopes.

## Primary Tools

- `open_project_session` — opens isolated session, returns bootstrap context
- `get_agent_bootstrap_context` — returns compact onboarding context without opening a session
- `get_current_project_context` — refreshes active project, version, mode, capabilities
- `describe_mcp_tooling` — reads tool manifest early when writes are anticipated

## Session Checklist

- [ ] project name and version known
- [ ] project mode (Design / LiveProtected) known
- [ ] capabilities (packages, node categories, permissions) known
- [ ] risk policy (confirmation thresholds, snapshot requirements) known
- [ ] resource links (documentation URLs) captured
- [ ] session identity preserved

## Standard Workflow

```text
open_project_session or get_agent_bootstrap_context
-> get_current_project_context (verify active context)
-> describe_mcp_tooling (if writes anticipated)
-> choose catalog / graph / governance workflow
```

## Anti-Patterns

- Guessing active project or version
- Mutating before opening a session
- Calling Direct MCP `connect_project` while an AgentReady session is active
- Using Direct MCP `/mcp` just because it has more tools
- Mixing context from `/mcp` and `/mcp/agent-ready/v1` silently

## Load Next Skill

- **Governance**: load `xtrader-governance` before any write or risky operation.
- **Catalog**: load `xtrader-catalog` when searching nodes, types, or patterns.
- **Types**: load `xtrader-types` when type details, compatibility, object/enum types, or type mutation are involved.
- **Nodes**: load `xtrader-nodes` when node schema, form data, generic params, or array port types are involved.
- **Visual graphs**: load `xtrader-visual-graphs` when VisualNode, FlowGraph, nested visual nodes, public port nodes, or port kinds are involved.
- **Graph plan**: load `xtrader-graph-plan` when creating or editing graphs.
- **Backtests**: load `xtrader-backtests` when the user asks to run, inspect, debug, or summarize backtests.
- **Direct**: load `xtrader-direct` only when AgentReady v1 lacks the required capability.
