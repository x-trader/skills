# Example: Open Project Session

**Endpoint**: `/mcp/agent-ready/v1`

**Skills**: `xtrader-mcp-agent-ready-session`

## Sequence

1. Call `open_project_session` with project identifier.
2. Inspect returned bootstrap: project name, version, mode, capabilities, risk policy, session ID.
3. Call `get_current_project_context` to verify active context.
4. If writes are anticipated, call `describe_mcp_tooling` to read tool manifest.
5. Decide next workflow based on task.

## Expected Output

```
open_project_session -> returns bootstrap context
get_current_project_context -> confirms project=MyStrategy, version=v2, mode=Design
describe_mcp_tooling -> returns manifest with risk metadata
```

## Key Checks

- [ ] Session identity preserved across calls.
- [ ] Project mode and capabilities captured.
- [ ] No catalog/graph/governance tools called before session is open.
- [ ] Direct MCP not used for session setup.
