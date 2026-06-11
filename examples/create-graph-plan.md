# Example: Create and Apply Graph Plan

**Endpoint**: `/mcp/agent-ready/v1`

**Skills**: `xtrader-mcp-agent-ready-session`, `xtrader-mcp-agent-ready-catalog`, `xtrader-mcp-agent-ready-graph-plan`, `xtrader-mcp-agent-ready-governance`

## Sequence

1. Verify active session via `get_current_project_context`.
2. Resolve intent and search catalog for target nodes (see `find-node-for-intent` example).
3. Call `check_port_compatibility` for desired connections.
4. If a known pattern exists, call `instantiate_graph_pattern(patternId, parameters)`.
5. If building manually, construct an operation-based plan:
   - `addGraphNode` for new node
   - `connectPorts` for edges
   - `setNodeFormData` for configuration
6. Call `validate_graph_plan(plan)`.
7. Inspect validation result for errors or warnings.
8. If errors found: repair plan and re-validate.
9. Load governance and satisfy requirements:
   - Check project mode
   - Create snapshot if policy requires
   - Request confirmation if policy requires
10. Call `apply_graph_plan(planId)`.
11. Verify changes with `get_current_project_context`.

## Expected Output

```
validate_graph_plan -> valid=true, warnings=[], planId=plan-123
describe_mcp_tooling -> risk=High, requiresConfirmation=true, requiresSnapshot=true
create_graph_snapshot -> snapshot=snap-456
[user confirms] -> confirmed=true
apply_graph_plan(plan-123) -> applied=true, changes=[added SmaAlert, connected to NotificationSender]
```

## Key Checks

- [ ] Validation called before apply.
- [ ] No `replace_graph` used for a small change.
- [ ] Governance requirements satisfied before apply.
- [ ] Changes explained as operations, not raw graph dump.
