# Example: Find Node for Intent

**Endpoint**: `/mcp/agent-ready/v1`

**Skills**: `xtrader-mcp-agent-ready-session`, `xtrader-mcp-agent-ready-catalog`

## Sequence

1. Ensure active session via `open_project_session` or verify with `get_current_project_context`.
2. Call `resolve_intent_concepts("notify when price crosses SMA threshold")`.
3. Inspect returned concepts: `["notification", "threshold", "moving_average", "condition"]`.
4. Call `suggest_nodes_for_intent` with resolved concepts.
5. Review candidates: check package availability, port direction/type, form data requirements.
6. Call `check_port_compatibility` for selected source/target node and port pairs.
7. If incompatible, call `suggest_adapter_nodes`.
8. Pass selected candidates to graph plan workflow.

## Expected Output

```
resolve_intent_concepts -> [notification, threshold, moving_average, condition]
suggest_nodes_for_intent -> [SmaAlert, PriceCrossCondition, NotificationSender]
check_port_compatibility(SmaAlert.output, NotificationSender.input) -> compatible=true
```

## Key Checks

- [ ] No node codes guessed from memory.
- [ ] Full catalog not dumped into context.
- [ ] Port compatibility checked before connections assumed.
- [ ] Adapter nodes suggested when ports are incompatible.
