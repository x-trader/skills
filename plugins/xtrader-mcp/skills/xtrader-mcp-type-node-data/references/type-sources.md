# Type Sources

XTrader MCP type references can come from three sources:

| Source | Meaning | Guidance |
|---|---|---|
| Project | User-defined type in the active project version | Safest to edit only after usage/impact analysis |
| Package | Type supplied by a package dependency | Do not mutate package types through project workflows |
| System | Primitive/system type exposed by MCP metadata | Treat as read-only |

Search project context first. Use package/system types only when returned by MCP discovery or compatibility tools.

Do not assume inheritance or base-type behavior. If MCP metadata returns base-type information, preserve it and validate compatibility. If metadata does not return it, treat the type as independent.
