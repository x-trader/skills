---
name: xtrader-catalog
description: Use this skill when selecting or understanding XTrader nodes, types, ports, packages, graph patterns, or adapters. Searches the AgentReady semantic catalog, resolves user intent into concepts, finds matching nodes/patterns, and checks port compatibility.
---

# XTrader Catalog Skill

Load this skill when the task requires finding or evaluating nodes, types, or graph patterns.

## Core Rules

1. Never guess node codes or invent node names from memory.
2. Never dump the full catalog into prompt context.
3. Search project-scoped catalog first (`search_catalog`). Use installable/global search only when results are insufficient.
4. Use catalog result details for selected candidates. If full node schema is required, load `xtrader-nodes`; if full type details are required, load `xtrader-types`. Use Direct fallback only when needed.
5. Check port compatibility (`check_port_compatibility`) before recommending graph connections.
6. Suggest adapter nodes (`suggest_adapter_nodes`) when ports are incompatible.
7. Prefer semantic concept workflows (`resolve_intent_concepts`, `suggest_nodes_for_intent`) for abstract user intent.

## Use Case: Intent to Concepts

User describes a goal in natural language.

```
resolve_intent_concepts("notify when price crosses threshold")
-> inspect returned concepts: ["notification", "threshold", "condition"]
-> search_catalog with refined concepts
-> suggest_nodes_for_intent with concepts
```

## Use Case: Concepts to Nodes

You have resolved concepts and need candidate nodes.

```
search_catalog(query, scope: project)
-> inspect candidate node summaries
-> load xtrader-nodes if full node schema, form data, or type params are needed
-> check_port_compatibility(source_node, target_node, source_port, target_port)
-> suggest_adapter_nodes if compatibility fails
```

## Use Case: Composition

User wants a multi-node pattern or reusable graph structure.

```
search_graph_patterns(intent or keywords)
-> inspect pattern summaries
-> instantiate_graph_pattern(patternId, parameters)
-> pass plan to graph plan workflow
```

## Result-Selection Heuristics

Evaluate candidates on:

- **Package availability**: is the providing package already installed?
- **Node source**: project node, installed package, or global catalog?
- **Required form data**: does the node need configuration values?
- **Port direction/type**: do input/output ports match?
- **Adapter requirements**: are adapter nodes needed between incompatible ports?
- **Type/node detail depth**: is catalog summary enough, or is Direct fallback needed for full schema?

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
-> search_graph_patterns if composition needed
-> select candidate nodes
-> check_port_compatibility
-> suggest_adapter_nodes if needed
-> pass selected candidates to graph plan workflow
```

## Anti-Patterns

- Inventing node names from memory
- Selecting nodes by title only without checking ports
- Skipping compatibility checks
- Recommending package installs without explaining why
- Ignoring package version when evaluating candidates
- Treating `get_node_details` as an AgentReady MCP v1 tool

## Load Next Skill

- **Graph plan**: load `xtrader-graph-plan` after node/port selection.
- **Types**: load `xtrader-types` for full type details, compatibility, object/enum types, or type mutation.
- **Nodes**: load `xtrader-nodes` for full node schema, form data, generic params, or array port types.
- **Governance**: load `xtrader-governance` before any apply.
- **Session**: load `xtrader-session` first if no active session.
