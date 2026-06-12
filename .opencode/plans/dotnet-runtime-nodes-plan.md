# Plan: Document .NET Runtime Nodes for Agent Knowledge

## Overview

The XTrader MCP metadata pipeline extracts the entire .NET BCL as nodes. Every public class, struct, interface, and enum from the .NET SDK reference assemblies becomes available as nodes with structured naming conventions. Agents need this knowledge to predict node names when searching the catalog.

## Changes

### 1. New file: `plugins/xtrader-mcp/skills/xtrader-nodes/references/dotnet-runtime-nodes.md`

Full reference covering:
- Package grouping (each assembly = one package: System.Runtime, System.Collections, System.Linq, etc.)
- Node naming table: constructors (`Create List<T>`), methods (`Add List<T>`), property getters (`Get Count of List<T>`), property setters (`Set Capacity of List<T>`), enum constants (`DayOfWeek.Sunday`), enum parse (`Parse DayOfWeek`), flags compose/split (`Compose BindingFlags Flags`)
- Humanization rules (PascalCase→spaced: `TryParse`→`Try Parse`)
- Excluded types (Attributes, compiler-generated, non-public, delegates, `[Node]` types)
- Excluded members (Comparer property, IComparer/Span/CultureInfo return types, indexers)
- Common .NET packages list with namespace mappings

### 2. Update: `docs/type-node-concepts.md`

Add a "## .NET Runtime Nodes" section after the "Type Kinds" section:

```markdown
## .NET Runtime Nodes

Every public .NET BCL type (class, struct, interface, enum) from the SDK reference assemblies
is extracted as nodes. Each assembly becomes a package (System.Runtime, System.Collections, etc.).
Node display names follow structured naming conventions. See the
[dotnet-runtime-nodes reference](plugins/xtrader-mcp/skills/xtrader-nodes/references/dotnet-runtime-nodes.md)
for the full naming table, package list, and exclusion rules.
```

### 3. Update: `plugins/xtrader-mcp/skills/xtrader-types/references/type-sources.md`

Expand the "System" source row:

```markdown
| System | Primitive/system type exposed by MCP metadata, including all .NET BCL types extracted from SDK reference assemblies | Treat as read-only. See the dotnet-runtime-nodes reference for naming conventions and package grouping. |
```

### 4. Update: `plugins/xtrader-mcp/skills/xtrader-nodes/SKILL.md`

Add a new section "## .NET Runtime Node Knowledge" before "## AgentReady-First Workflow":

```markdown
## .NET Runtime Node Knowledge

The entire .NET BCL is available as nodes. Agents should use knowledge of .NET type names
and member patterns to predict node display names:

- Constructor: `Create {TypeName}` (e.g., `Create List<T>`)
- Method: `{MethodName} {TypeName}` (e.g., `Add List<T>`, `Parse Int32`)
- Property getter: `Get {PropertyName} of {TypeName}` (e.g., `Get Count of List<T>`)
- Property setter: `Set {PropertyName} of {TypeName}` (e.g., `Set Capacity of List<T>`)
- Enum constant: `{TypeName}.{MemberName}` (e.g., `DayOfWeek.Sunday`)
- Enum parse: `Parse {TypeName}` / `Try Parse {TypeName}`
- Flags compose: `Compose {TypeName} Flags` / `Split {TypeName} Flags`

Each assembly is its own package folder (System.Runtime, System.Collections, System.Linq, etc.).
See the [dotnet-runtime-nodes](references/dotnet-runtime-nodes.md) reference for the full
naming table, package list, exclusions, and search guidance.
```

## Verification

1. Confirm `dotnet-runtime-nodes.md` contains all naming patterns, package grouping, exclusion rules, and search guidance
2. Confirm `type-node-concepts.md` new section references the new file
3. Confirm `type-sources.md` System row mentions BCL extraction
4. Confirm `SKILL.md` has .NET Runtime Node Knowledge section before AgentReady-First Workflow
