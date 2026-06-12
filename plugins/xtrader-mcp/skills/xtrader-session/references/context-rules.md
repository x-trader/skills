# Context Rules

## Session Context (AgentReady)

- Opened via `open_project_session`.
- Scoped to the agent's conversation session.
- Includes session ID, project context, and governance state.
- Lost on session timeout or if the server resets.
- `get_current_project_context` refreshes the active session context.

## User Context (Direct MCP)

- Established via `connect_project`.
- Scoped to the authenticated user, not the agent session.
- Persists across agent conversations for the same user.
- `get_current_project_context` on Direct MCP returns Direct MCP context.

## Critical Rule

Do not mix context from the two surfaces. If you start on AgentReady, stay on AgentReady. If you fall back to Direct MCP, refresh AgentReady context when you return.

**AgentReady `get_current_project_context`** returns session-scoped data such as session ID and governance state.
**Direct MCP `get_current_project_context`** returns user-scoped Direct MCP context.
