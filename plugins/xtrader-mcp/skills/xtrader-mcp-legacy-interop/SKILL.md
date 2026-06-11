---
name: xtrader-mcp-legacy-interop
description: Use only when XTrader AgentReady MCP v1 does not expose the required capability and the agent must use the legacy /mcp surface. Guides controlled fallback to legacy tools while warning about user-scoped context, broader direct mutation tools, and higher governance risk.
---

# XTrader MCP Legacy Interop Skill

Use this skill only as a fallback.

Default endpoint:

```text
/mcp/agent-ready/v1
```

Legacy endpoint:

```text
/mcp
```

## When to Use Legacy

Use legacy only when AgentReady v1 lacks required capability, such as legacy-only backtest tools, package dependency tools, detailed project version tools, detailed graph read tools, or confirmation tools.

## Core Rules

1. Prefer AgentReady v1.
2. Explain why legacy fallback is needed.
3. Connect legacy context with `connect_project`.
4. Remember legacy context is user-scoped, not session-isolated.
5. Prefer read-only legacy tools.
6. For writes, require plan, validation, snapshot, and confirmation when available.
7. Return to AgentReady workflow after fallback.

## Legacy Context Warning

Legacy `get_current_project_context` is not the same as AgentReady `get_current_project_context`.

Do not mix them silently.

## Anti-Patterns

Do not use legacy because it is easier, perform direct legacy mutation when AgentReady has graph plan tools, ignore legacy context isolation limitations, or use legacy as the default endpoint.
