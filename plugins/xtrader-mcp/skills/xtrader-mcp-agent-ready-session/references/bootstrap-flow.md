# Bootstrap Flow

Preferred first calls: `open_project_session` or `get_agent_bootstrap_context`.

`open_project_session`:
- Opens an isolated session scoped to the agent.
- Returns project, version, mode, capabilities, risk policy, session identity, and resource links.
- Requires project identifier and optional version.

`get_agent_bootstrap_context`:
- Returns a compact onboarding context without creating a session.
- Useful for quick lookups or discovery before committing to a session.

After either call, use `get_current_project_context` to verify and refresh the active context.

Track from the output:
- **project name/version**: what you are working on
- **project mode**: Design or LiveProtected
- **capabilities**: installed packages, node categories, permissions
- **risk policy**: confirmation thresholds, snapshot requirements
- **session identity**: session ID for follow-up calls
