---
name: xtrader-mcp-direct-fallback
description: Use only when XTrader AgentReady MCP v1 does not expose the required capability and the agent must use the Direct MCP /mcp surface. Guides controlled fallback to Direct MCP tools while warning about user-scoped context, broader direct mutation tools, and higher governance risk.
---

# XTrader MCP Direct Fallback Skill

Use this skill only as a fallback.

Default endpoint:

```text
/mcp/agent-ready/v1
```

Direct MCP route:

```text
/mcp
```

AgentReady MCP v1 route:

```text
/mcp/agent-ready/v1
```

## When to Use Direct Fallback

Use Direct MCP only when AgentReady v1 lacks the required capability, such as execution/backtest tools, package dependency tools, detailed project version tools, detailed graph read tools, or confirmation tools not yet exposed through AgentReady.

## Core Rules

1. AgentReady MCP v1 is the default.
2. Use Direct MCP only when AgentReady v1 lacks the required capability.
3. Explain why fallback is needed.
4. Prefer read-only Direct MCP tools.
5. Direct MCP has broader low-level mutation tools.
6. Direct MCP context may differ from AgentReady session context.
7. Connect via `connect_project` when using Direct MCP.
8. For writes, require plan, validation, snapshot, and confirmation when available.
9. Return to AgentReady workflow after fallback.

## Direct MCP Context Warning

Direct MCP `get_current_project_context` is not the same as AgentReady `get_current_project_context`.

Do not mix them silently.

## Anti-Patterns

Do not use Direct MCP because it is easier, perform direct mutation when AgentReady has graph plan tools, ignore Direct MCP context isolation limitations, or use Direct MCP as the default endpoint.
