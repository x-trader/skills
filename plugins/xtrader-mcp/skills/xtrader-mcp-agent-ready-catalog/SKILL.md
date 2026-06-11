---
name: xtrader-mcp-agent-ready-catalog
description: Use when finding XTrader nodes, types, ports, packages, semantic concepts, installed capabilities, installable package capabilities, adapter nodes, compatibility, or graph patterns through AgentReady MCP. Guides agents to query the project-scoped semantic catalog instead of guessing node codes or dumping the full catalog.
---

# XTrader MCP AgentReady Catalog Skill

Use this skill whenever the task requires selecting or understanding nodes, types, ports, packages, concepts, or graph patterns.

## Core Rules

1. Never guess node codes.
2. Never dump the full catalog.
3. Search project-scoped catalog first.
4. Use installable/global search only when installed catalog has no suitable candidate.
5. Get details only for selected candidates.
6. Check port compatibility before recommending graph connections.
7. Suggest adapter nodes when ports are incompatible.
8. Prefer semantic concept and pattern workflows for abstract user intent.

## Primary Tools

- `search_catalog`
- `resolve_intent_concepts`
- `suggest_nodes_for_intent`
- `check_port_compatibility`
- `suggest_adapter_nodes`
- `search_graph_patterns`
- `instantiate_graph_pattern`

## Standard Workflow

```text
resolve_intent_concepts
-> search_catalog or suggest_nodes_for_intent
-> search_graph_patterns if composition is needed
-> select candidate nodes
-> check_port_compatibility
-> suggest_adapter_nodes if needed
-> pass selected candidates to graph plan workflow
```

## Anti-Patterns

Do not invent node names from memory, select nodes only by title without checking ports, skip compatibility checks, or recommend installing packages without explaining why.
