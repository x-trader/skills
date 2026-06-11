# XTrader MCP Plugin

This plugin contains MCP-only skills for XTrader.

## MCP Surfaces

### AgentReady v1

```text
/mcp/agent-ready/v1
```

Use this by default for agents.

Primary capabilities:

- isolated project session
- bootstrap context
- tool manifest
- semantic catalog
- graph pattern search
- graph plan validation/apply
- governance metadata

### Legacy MCP

```text
/mcp
```

Use only as a controlled fallback.

Legacy has broader tool coverage but more direct mutation tools and weaker session isolation.

## Skills

```text
skills/xtrader-mcp-agent-ready-session
skills/xtrader-mcp-agent-ready-catalog
skills/xtrader-mcp-agent-ready-graph-plan
skills/xtrader-mcp-agent-ready-governance
skills/xtrader-mcp-legacy-interop
```
