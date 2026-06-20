# XTrader MCP Skills

Agent skills for working with XTrader MCP surfaces.

This repository is intentionally focused on MCP agent workflows only.

Default MCP surface for agents:

```text
/mcp/agent-ready/v1
```

Direct MCP surface:

```text
/mcp
```

Use the Direct MCP surface only when AgentReady v1 does not expose the required capability.

## Plugin

```text
plugins/xtrader-mcp
```

## Skills

- `xtrader-session`
- `xtrader-catalog`
- `xtrader-types`
- `xtrader-nodes`
- `xtrader-core-nodes`
- `xtrader-visual-graphs`
- `xtrader-graph-plan`
- `xtrader-governance`
- `xtrader-backtests`
- `xtrader-direct`

## Design Principles

- AgentReady v1 is the default surface for agents.
- Direct MCP is a controlled fallback / trusted low-level surface.
- Skills guide agents; they do not replace MCP tools, validation, confirmation, or governance.
- Never dump the full catalog into prompt context.
- Never dump full backtest logs, drawings, or positions into prompt context.
- Never guess node codes.
- Use Core node display names from `xtrader-core-nodes` when searching built-in visual scripting nodes.
- Never invent visual-node public ports outside official Core IO public port nodes.
- Prefer plans, validation, governance, and controlled apply flows.
