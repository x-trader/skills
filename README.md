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

- `xtrader-mcp-agent-ready-session`
- `xtrader-mcp-agent-ready-catalog`
- `xtrader-mcp-type-node-data`
- `xtrader-mcp-agent-ready-graph-plan`
- `xtrader-mcp-agent-ready-governance`
- `xtrader-mcp-direct-fallback`

Future optional skill:

- `xtrader-mcp-agent-ready-execution`

## Design Principles

- AgentReady v1 is the default surface for agents.
- Direct MCP is a controlled fallback / trusted low-level surface.
- Skills guide agents; they do not replace MCP tools, validation, confirmation, or governance.
- Never dump the full catalog into prompt context.
- Never guess node codes.
- Prefer plans, validation, governance, and controlled apply flows.
