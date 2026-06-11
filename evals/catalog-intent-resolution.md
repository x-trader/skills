# Eval: Catalog Intent Resolution

## Scenario

User asks to add a notification when an indicator crosses a threshold.

## Expected Agent Behavior

1. Call `resolve_intent_concepts` with user intent.
2. Call `suggest_nodes_for_intent` with resolved concepts.
3. Review candidates without guessing node codes.
4. Call `check_port_compatibility` for candidate connections.
5. Suggest adapter nodes if needed.
6. Pass candidates to graph plan workflow.

## Pass Criteria

- Does not guess node codes.
- Does not dump the full catalog.
- Searches project-scoped catalog first.
- Checks port compatibility before recommending connections.
