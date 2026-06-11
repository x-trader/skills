# Backend Source Map

Key implementation files in the XTrader MCP server.

## Routing & Filtering

| File | Purpose |
|---|---|
| `src/.../Projects.Mcp/Router.cs` | Server setup, DI registration, endpoint mapping, tool filtering per route |
| `src/.../AgentReady/V1/ProjectsMcpAgentReadyV1Constants.cs` | Route constant, surface name constant |

## Tool Files

| Surface | File | Tools |
|---|---|---|
| Direct | `Tools/McpProjectTools.cs` | `connect_project`, `get_current_project_context`, `switch_project_version`, `describe_project_capabilities` |
| Direct | `Tools/McpPackageTools.cs` | 18 package tools |
| Direct | `Tools/McpTypeTools.cs` | 16 type tools |
| Direct | `Tools/McpNodeTools.cs` | 7 node tools |
| Direct | `Tools/McpGraphTools.cs` | 16 graph tools |
| Direct | `Tools/McpFolderTools.cs` | 3 folder tools |
| Direct | `Tools/McpProjectVersionTools.cs` | 4 version tools |
| Direct | `Tools/McpBacktestTools.cs` | 23 backtest tools |
| Direct | `Tools/McpConfirmationTools.cs` | 3 confirmation tools |
| AgentReady | `AgentReady/V1/Tools/McpAgentReadyProjectSessionTools.cs` | `open_project_session`, `get_agent_bootstrap_context`, `get_current_project_context` |
| AgentReady | `AgentReady/V1/Tools/McpAgentReadyToolingTools.cs` | `describe_mcp_tooling` |
| AgentReady | `AgentReady/V1/Tools/McpAgentReadyGraphPlanTools.cs` | `validate_graph_plan`, `apply_graph_plan` |
| AgentReady | `AgentReady/V1/Tools/McpAgentReadySemanticCatalogTools.cs` | 7 catalog tools |

## Metadata & Governance

| File | Purpose |
|---|---|
| `AgentReady/V1/Services/McpAgentReadyToolDescriptorRegistry.cs` | Tool risk, category, precondition, requirement metadata |

## Documentation

| File | Purpose |
|---|---|
| `docs/mcp/tools.md` | Full Direct MCP tool catalog |
| `docs/mcp/agent-ready/tool-manifest.md` | AgentReady tool manifest design |
| `docs/mcp/agent-ready/governance.md` | Governance design |
| `docs/mcp/agent-ready/session-context.md` | Session context design |
| `docs/mcp/agent-ready/bootstrap-context.md` | Bootstrap context design |
| `docs/mcp/agent-ready/plan-apply.md` | Graph plan lifecycle design |
| `docs/mcp/agent-ready/live-protection.md` | Live protection design |
| `docs/mcp/agent-ready/semantic-catalog-intelligence.md` | Semantic catalog design |
