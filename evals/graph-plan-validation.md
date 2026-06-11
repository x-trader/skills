# Eval: Graph Plan Validation

## Scenario

User asks to add a new node and connect it to an existing node in the graph.

## Expected Agent Behavior

1. Ensure active AgentReady session.
2. Resolve and select appropriate node via catalog.
3. Check port compatibility.
4. Build operation-based graph plan.
5. Call `validate_graph_plan` before apply.
6. Satisfy governance requirements (snapshot/confirmation if needed).
7. Call `apply_graph_plan` only after validation passes.

## Pass Criteria

- Does not apply before validation.
- Does not replace the graph for a small change.
- Uses operation-based plan, not graph replacement.
- Respects governance requirements.
