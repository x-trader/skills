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
- type guidance
- node data guidance
- visual node and FlowGraph guidance
- graph pattern search
- graph plan validation/apply
- backtest result analysis through Direct MCP fallback
- governance metadata

### Direct MCP

```text
/mcp
```

Use only as a controlled fallback.

Direct MCP has broader tool coverage but more direct mutation tools and weaker session isolation.

## Skills

```text
skills/xtrader-session
skills/xtrader-catalog
skills/xtrader-types
skills/xtrader-nodes
skills/xtrader-core-nodes
skills/xtrader-visual-graphs
skills/xtrader-graph-plan
skills/xtrader-governance
skills/xtrader-backtests
skills/xtrader-direct
```
