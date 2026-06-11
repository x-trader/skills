# Eval: Catalog Intent Resolution

**Skills under test**: `xtrader-mcp-agent-ready-session`, `xtrader-mcp-agent-ready-catalog`

## Scenario

User asks: "Add a notification that triggers when an indicator crosses above a threshold."

## Expected Agent Behavior

1. Ensure active AgentReady session via `get_current_project_context`.
2. Call `resolve_intent_concepts` with user's natural language intent.
3. Call `suggest_nodes_for_intent` with resolved concepts.
4. Review candidates without guessing node codes.
5. Call `check_port_compatibility` for selected source/target port pairs.
6. Suggest adapter nodes if ports are incompatible.
7. Pass candidates to graph plan workflow.

## Pass/Fail Rubric

| Criteria | Pass | Fail |
|---|---|---|
| Intent resolution | Calls `resolve_intent_concepts` with natural language | Guesses nodes without resolving intent |
| Node selection | Uses `suggest_nodes_for_intent` or `search_catalog` | Invents node names from memory |
| Catalog scope | Searches project-scoped catalog first | Dumps full catalog into context |
| Port compatibility | Calls `check_port_compatibility` before recommending connections | Assumes compatibility without checking |
| Adapter awareness | Calls `suggest_adapter_nodes` when ports are incompatible | Ignores port mismatch |
| Skill activation | Loads `xtrader-mcp-agent-ready-catalog` | Works without loading the skill |

## Negative Cases

| Case | Expected behavior |
|---|---|
| Agent guesses "SmaCrossNode" without searching | Fail — must search catalog |
| Agent lists every catalog entry in the response | Fail — must select candidates only |
| Agent skips port compatibility check | Fail — must check before connecting |
| Agent uses Direct MCP catalog search when AgentReady catalog exists | Fail — must use AgentReady first |
