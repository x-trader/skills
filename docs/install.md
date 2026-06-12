# Install

This repository is a skills pack for agents that use XTrader MCP.

## Setup

1. Clone this repository into your agent's skills directory.
2. Ensure the plugin path in `.agents/plugins/marketplace.json` resolves correctly for your agent runtime.
3. Verify the plugin loads:
   ```
   ls plugins/xtrader-mcp/skills/
   ```
   Expected output: nine skill directories.

## Activation

Skills are activated automatically when the task matches their `description` frontmatter. The recommended activation order is:

1. `xtrader-session`
2. `xtrader-governance`
3. `xtrader-catalog`
4. `xtrader-types` (when type details, object/enum types, compatibility, or type mutation are involved)
5. `xtrader-nodes` (when node schema, form data, input values, generic params, or array port types are involved)
6. `xtrader-visual-graphs` (when VisualNode, FlowGraph, nested visual nodes, public port nodes, or port kinds are involved)
7. `xtrader-graph-plan`
8. `xtrader-backtests` (for backtest execution or result analysis)
9. `xtrader-direct` (only when needed)

## Dependencies

- An agent runtime that supports Agent Skills
- Access to an XTrader MCP server exposing `/mcp/agent-ready/v1` and optionally `/mcp`
