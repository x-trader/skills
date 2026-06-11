# Example: Live Protected Change

**Endpoint**: `/mcp/agent-ready/v1`

**Skills**: `xtrader-mcp-agent-ready-session`, `xtrader-mcp-agent-ready-governance`, `xtrader-mcp-agent-ready-graph-plan`

## Sequence

1. Verify active session with `get_current_project_context` — note mode is `LiveProtected`.
2. Call `describe_mcp_tooling` to check risk metadata for intended tools.
3. Resolve intent and search catalog for the target node.
4. Call `instantiate_graph_pattern` or build a small operation-based plan.
5. Call `validate_graph_plan(plan)`.
6. If policy requires a snapshot and AgentReady does not expose snapshot creation, load Direct fallback and call `create_graph_snapshot` with explanation.
7. Require user confirmation before apply; if MCP confirmation tooling is required, load Direct fallback and call `confirm_action` with explanation.
8. Once confirmed, call `apply_graph_plan(planId)`.
9. Verify applied changes with `get_current_project_context`.
10. Summarize: what changed, snapshot ID, confirmation ID.

## Expected Output

```
get_current_project_context -> mode=LiveProtected
describe_mcp_tooling -> risk=High, requiresSnapshot=true, requiresConfirmation=true
instantiate_graph_pattern -> plan=plan-789
validate_graph_plan(plan-789) -> valid=true
[fallback if required] create_graph_snapshot -> snapshot=snap-456
[user confirms or fallback if required] confirm_action -> confirmed=true
apply_graph_plan(plan-789) -> applied=true, changes=[added OrderRouter]
get_current_project_context -> confirms graph updated
```

## Key Checks

- [ ] No silent mutation in LiveProtected mode.
- [ ] Snapshot created before mutation.
- [ ] User confirmation obtained before apply.
- [ ] Direct-only snapshot/confirmation tools used only through explicit Direct fallback.
- [ ] Changes explained clearly.
- [ ] Governance result summarized for user.
