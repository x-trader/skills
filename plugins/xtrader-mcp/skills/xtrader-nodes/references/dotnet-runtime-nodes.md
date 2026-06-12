# .NET Runtime Nodes

The XTrader MCP metadata pipeline extracts every public .NET BCL type from the .NET SDK reference assemblies. Each public class, struct, interface, and enum becomes available as nodes with structured display names. Use this knowledge to predict node names when searching the catalog or planning graph nodes.

## Package Grouping

Each .NET assembly is extracted as a separate package. Nodes are grouped by namespace → type name folder hierarchy.

| Package | Namespace Examples |
|---|---|
| `System.Runtime` | `System`, `System.Runtime`, `System.Runtime.CompilerServices` |
| `System.Collections` | `System.Collections`, `System.Collections.Generic` |
| `System.Collections.Concurrent` | `System.Collections.Concurrent` |
| `System.Linq` | `System.Linq` |
| `System.Linq.Expressions` | `System.Linq.Expressions` |
| `System.Text.RegularExpressions` | `System.Text.RegularExpressions` |
| `System.Text.Json` | `System.Text.Json`, `System.Text.Json.Serialization` |
| `System.IO` | `System.IO` |
| `System.IO.Compression` | `System.IO.Compression` |
| `System.Net.Http` | `System.Net.Http` |
| `System.Net.Primitives` | `System.Net`, `System.Net.NetworkInformation` |
| `System.Net.Sockets` | `System.Net.Sockets` |
| `System.Threading` | `System.Threading` |
| `System.Threading.Tasks` | `System.Threading.Tasks` |
| `System.Reflection` | `System.Reflection` |
| `System.Console` | `System` (Console, ConsoleColor) |
| `System.Data.Common` | `System.Data` |
| `System.Security.Cryptography` | `System.Security.Cryptography` |
| `System.Xml.ReaderWriter` | `System.Xml` |
| `System.Xml.Linq` | `System.Xml.Linq` |
| `System.Memory` | `System`, `System.Buffers` |
| `System.Numerics.Vectors` | `System.Numerics` |
| `System.ComponentModel` | `System.ComponentModel` |

Folder path for a node: `{Namespace}.{TypeName}` — e.g., `System.Collections.Generic.List<T>` maps to folder hierarchy `System` > `System.Collections` > `System.Collections.Generic` > `System.Collections.Generic.List<T>`.

## Node Naming Conventions

### Constructors

| Pattern | Examples |
|---|---|
| `Create {TypeName}` | `Create List<T>`, `Create String`, `Create DateTime`, `Create StreamReader` |

### Methods

| Pattern | Examples |
|---|---|
| `{MethodName} {TypeName}` | `Add List<T>`, `Contains List<T>`, `Sort List<T>`, `ReadLine StreamReader`, `Parse Int32` |

Method names are humanized:
- PascalCase → spaced: `TryParse` → `Try Parse`, `IndexOf` → `Index Of`, `GetHashCode` → `Get Hash Code`
- Underscores → spaces
- Interface prefix `I` preserved (`IComparable`, `IEnumerable`)

### Property Getters

| Pattern | Examples |
|---|---|
| `Get {PropertyName} of {TypeName}` | `Get Count of List<T>`, `Get Length of String`, `Get Capacity of List<T>` |

### Property Setters

| Pattern | Examples |
|---|---|
| `Set {PropertyName} of {TypeName}` | `Set Capacity of List<T>`, `Set Position of StreamReader` |

### Enum Constants

| Pattern | Examples |
|---|---|
| `{TypeName}.{MemberName}` | `DayOfWeek.Sunday`, `StringComparison.OrdinalIgnoreCase`, `BindingFlags.Public`, `ConsoleColor.Red` |

### Enum Parse

| Pattern | Examples |
|---|---|
| `Parse {TypeName}` | `Parse DayOfWeek`, `Parse ConsoleColor`, `Parse StringComparison` |
| `Try Parse {TypeName}` | `Try Parse DayOfWeek`, `Try Parse ConsoleColor` |

### Enum Numeric Conversion

| Pattern | Examples |
|---|---|
| `To Number {TypeName}` | `To Number DayOfWeek`, `To Number BindingFlags` |

### Flags Enum (only for `[Flags]` enums)

| Pattern | Examples |
|---|---|
| `Compose {TypeName} Flags` | `Compose BindingFlags Flags`, `Compose AttributeTargets Flags` |
| `Split {TypeName} Flags` | `Split BindingFlags Flags`, `Split AttributeTargets Flags` |

## Excluded Types

Filtered out during extraction:
- Anonymous types
- Non-public types
- Types that are not Class, Struct, Interface, or Enum (delegates, pointers)
- Compiler-generated types starting with `<`
- Types ending with `Attribute` (e.g., `ObsoleteAttribute`)
- Non-generic types containing `<` in display name
- Visual scripting nodes (inherit from `Node`/`FlowableNode`/`PortNode` or annotated with `[Node]`)

## Excluded Members

- Non-public constructors, methods, properties
- Implicit/compiler-generated members
- Operator overloads, event add/remove
- Indexer getters/setters (`get_Item` / `set_Item`)
- `Comparer` property
- Return types ignored: `IComparer`, `Converter`, `CultureInfo`, `IEqualityComparer`, `IFormatProvider`, `Span`, `ReadOnlySpan`, `StringRuneEnumerator`, `CharEnumerator`, `Comparison`

## Agent Usage

- Search for nodes by their **display name**: `"Sort List<T>"` not `"List.Sort"`
- Search for property nodes as `"Get Count of List<T>"` or `"Set Capacity of List<T>"`
- Search for enum constants as `"DayOfWeek.Sunday"` or `"StringComparison.Ordinal"`
- Enum parse nodes are `"Parse DayOfWeek"` not `"Enum.Parse"`
- The package field tells you which assembly a node comes from (e.g., `System.Runtime`, `System.Collections`)
- Generic names like `List<T>` appear with `<T>` suffix in display names
- Load this reference when entering the `xtrader-nodes` skill — the naming patterns are essential for accurate catalog searches
