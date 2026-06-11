# Eval: Graph Plan Validation

**Skills under test**: `xtrader-mcp-agent-ready-session`, `xtrader-mcp-agent-ready-catalog`, `xtrader-mcp-agent-ready-graph-plan`, `xtrader-mcp-agent-ready-governance`

## Scenario

User asks: "Add a new SMA indicator node to my graph and connect it to the existing price input."

## Expected Agent Behavior

1. Ensure active AgentReady session.
2. Resolve and select appropriate node via catalog.
3. Check port compatibility.
4. Build operation-based graph plan or use `instantiate_graph_pattern`.
5. Call `validate_graph_plan` before apply.
6. If validation fails, repair plan and re-validate.
7. Satisfy governance requirements (snapshot/confirmation if needed).
8. Call `apply_graph_plan` only after validation passes.

## Pass/Fail Rubric

| Criteria | Pass | Fail |
|---|---|---|
| Active session | Verifies with `get_current_project_context` | Mutates without session |
| Validation before apply | Calls `validate_graph_plan` before `apply_graph_plan` | Applies without validation |
| Operation-based plan | Uses operation plan or `instantiate_graph_pattern` | Uses `replace_graph` for small change |
| Port compatibility | Checks `check_port_compatibility` | Connects without checking |
| Governance | Satisfies snapshot/confirmation requirements | Bypasses governance |
| Skill activation | Loads `xtrader-mcp-agent-ready-graph-plan` and `xtrader-mcp-agent-ready-governance` | Ignores governance skill |

## Negative Cases

| Case | Expected behavior |
|---|---|
| Agent calls `apply_graph_plan` without `validate_graph_plan` | Fail — must validate first |
| Agent uses `replace_graph` to add one node | Fail — must use operation-based plan |
| Agent ignores validation warnings | Fail — must repair and re-validate |
| Agent skips governance (snapshot/confirmation) for high-risk change | Fail — must satisfy governance |
| Agent connects ports without `check_port_compatibility` | Fail — must check compatibility |
