---
name: xtrader-mcp-agent-ready-session
description: Use when connecting to XTrader AgentReady MCP, opening or reading a project session, selecting project/version, reading bootstrap context, understanding project capabilities, or preparing any MCP workflow on /mcp/agent-ready/v1.
---

# XTrader MCP AgentReady Session Skill

Use this skill before any serious XTrader MCP workflow.

Default agent endpoint:

```text
/mcp/agent-ready/v1
```

## Core Rules

1. Start with `open_project_session` or `get_agent_bootstrap_context`.
2. Do not call catalog, graph, or apply tools before an active AgentReady session exists.
3. Use `get_current_project_context` to refresh session context.
4. Read `describe_mcp_tooling` early when planning writes.
5. Track project mode and capabilities from bootstrap output.
6. Preserve session identity when making follow-up calls.

## Primary Tools

- `open_project_session`
- `get_agent_bootstrap_context`
- `get_current_project_context`
- `describe_mcp_tooling`

## Standard Workflow

```text
open_project_session or get_agent_bootstrap_context
-> inspect project/version/mode/capabilities
-> describe_mcp_tooling
-> choose catalog/graph/governance workflow
```

## Anti-Patterns

Do not guess active project context, mutate before opening a session, mix AgentReady and legacy contexts silently, or use legacy `/mcp` just because it has more tools.
