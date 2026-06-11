# Install

This repository is a skills pack for agents that use XTrader MCP.

## Setup

1. Clone this repository into your agent's skills directory.
2. Ensure the plugin path in `.agents/plugins/marketplace.json` resolves correctly for your agent runtime.
3. Verify the plugin loads:
   ```
   ls plugins/xtrader-mcp/skills/
   ```
   Expected output: seven skill directories.

## Activation

Skills are activated automatically when the task matches their `description` frontmatter. The recommended activation order is:

1. `xtrader-mcp-agent-ready-session`
2. `xtrader-mcp-agent-ready-governance`
3. `xtrader-mcp-agent-ready-catalog`
4. `xtrader-mcp-type-node-data` (when type details, node schema, form data, or generic params are involved)
5. `xtrader-mcp-agent-ready-graph-plan`
6. `xtrader-mcp-backtest-results` (for backtest execution or result analysis)
7. `xtrader-mcp-direct-fallback` (only when needed)

## Dependencies

- An agent runtime that supports Agent Skills
- Access to an XTrader MCP server exposing `/mcp/agent-ready/v1` and optionally `/mcp`
