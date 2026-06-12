---
name: xtrader-backtests
description: Use this skill when a user asks to run, inspect, compare, debug, or summarize XTrader backtests or backtest results. Guides creation, polling, result summaries, issues, logs, symbols, positions, drawings, and focused drilldowns through Direct MCP fallback.
---

# XTrader Backtests Skill

Load this skill for backtest execution or result analysis.

AgentReady MCP v1 remains the default. Backtest tools are Direct MCP-only today, so explain fallback before using `/mcp`.

## Core Rules

1. Start from AgentReady session context, then fall back to Direct MCP only because AgentReady v1 lacks backtest tools.
2. Explain fallback before calling Direct MCP backtest tools.
3. Call `connect_project` on Direct MCP before creating or reading backtests.
4. Prefer summary/snapshot tools before raw logs, drawings, or full position lists.
5. Do not dump full logs, drawings, or positions into prompt context.
6. Drill down only after identifying relevant symbol, position, time range, or issue.
7. Do not mutate graph, type, node, or package state while inspecting results.
8. Return to AgentReady MCP v1 and refresh context after backtest work.

## Primary Workflow

```text
get_current_project_context on AgentReady
-> explain Direct MCP fallback for backtest
-> connect_project on /mcp
-> create_backtest or list_backtests
-> wait_backtest if newly created
-> get_backtest_overview
-> get_backtest_snapshot
-> get_backtest_issues
-> get_backtest_results_summary
-> drill into symbols/positions/logs only as needed
-> summarize findings
-> return to AgentReady and refresh context
```

## Primary Tools

- `create_backtest`
- `wait_backtest`
- `list_backtests`
- `get_backtest`
- `get_backtest_overview`
- `get_backtest_snapshot`
- `get_backtest_issues`
- `get_backtest_results_summary`
- `get_backtest_timeline`
- `query_backtest_results`
- `search_backtest_logs`

## Drilldown Tools

- `list_trade_sessions`
- `list_backtest_symbols`
- `get_backtest_symbol`
- `get_backtest_symbol_snapshot`
- `list_backtest_logs`
- `list_backtest_drawings`
- `list_backtest_positions`
- `get_backtest_positions_summary`
- `get_backtest_positions_win_rate`
- `get_backtest_position`
- `get_backtest_position_snapshot`
- `get_backtest_position_shapes`

## Result Summary Checklist

- [ ] completion/progress state
- [ ] total symbols and processed symbols
- [ ] position counts
- [ ] win/loss or win-rate summary when available
- [ ] major issues from `get_backtest_issues`
- [ ] high-signal logs only, not full log dumps
- [ ] symbols with unusual behavior
- [ ] notable positions or failures
- [ ] next investigation steps

## Anti-Patterns

- Using Direct MCP without explaining fallback
- Creating a backtest and not waiting or polling
- Reading raw logs before overview/snapshot/issues
- Dumping full logs, drawings, or all positions
- Ignoring `get_backtest_issues`
- Mutating graph/package/type/node state during result analysis
- Staying on Direct MCP after backtest work completes

## Load Next Skill

- **Session**: load `xtrader-session` before and after Direct fallback.
- **Direct**: load `xtrader-direct` before using `/mcp` backtest tools.
- **Governance**: load `xtrader-governance` if a backtest request includes any write or live/protected concern beyond result inspection.
