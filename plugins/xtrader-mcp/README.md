# XTrader MCP Plugin

This plugin contains MCP-only skills for XTrader.

## MCP Surfaces

### AgentReady MCP v1

```text
/mcp/agent-ready/v1
```

Use this by default for agents.

Primary capabilities:

- isolated project session
- bootstrap context
- tool manifest
- semantic catalog
- type and node data guidance
- graph pattern search
- graph plan validation/apply
- governance metadata

### Direct MCP

```text
/mcp
```

Use only as a controlled fallback.

Direct MCP has broader tool coverage but more direct mutation tools and weaker session isolation.

## Skills

```text
skills/xtrader-mcp-agent-ready-session
skills/xtrader-mcp-agent-ready-catalog
skills/xtrader-mcp-type-node-data
skills/xtrader-mcp-agent-ready-graph-plan
skills/xtrader-mcp-agent-ready-governance
skills/xtrader-mcp-direct-fallback
```
