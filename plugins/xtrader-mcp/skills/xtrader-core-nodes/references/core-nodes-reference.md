# Core Nodes Reference

Core nodes are the built-in visual scripting nodes from the `XTrader.Nodes.Core` package. Use this reference to choose the right node family before searching the MCP catalog or building a graph plan.

Core nodes are different from .NET runtime nodes. Do not search for them with .NET runtime patterns like `Create List<T>` or `Add List<T>`. Search by Core node display names such as `If`, `ForEach`, `Addition`, `Mapper`, or `ValueInputPort`.

## IO / Public Port Nodes

Use these nodes inside a visual node graph to expose public inputs and outputs.

| Display name | Purpose |
|---|---|
| `ValueInputPort` | Creates a public typed value input for the visual node. |
| `ValueOutputPort` | Creates a public typed value output for the visual node. |
| `SignalInputPort` | Creates a public signal input with no payload. |
| `SignalOutputPort` | Creates a public signal output with no payload. |
| `FlowInputPort` | Creates a public flow input with a typed payload. |
| `FlowOutputPort` | Creates a public flow output with a typed payload. |

Agent notes:

- Set the public port name through the node's `Name` input value.
- Set value/flow port type params from returned node schema only.
- Load `xtrader-visual-graphs` when exposing visual-node public ports.

## Math

Use math nodes for typed numeric operations.

| Display name | Purpose |
|---|---|
| `Addition` | Adds two numeric values. |
| `Subtraction` | Subtracts the second numeric value from the first. |
| `Multiplication` | Multiplies two numeric values. |
| `Division` | Divides the first numeric value by the second. |

Agent notes:

- These nodes are typed. Use returned schema/type params to bind `Int32`, `Double`, `Decimal`, or another supported numeric type.
- Check port compatibility before connecting numeric inputs or outputs.

## Logic

Use logic nodes for boolean decisions and conditional values.

| Display name | Purpose |
|---|---|
| `And` | Returns true when both boolean inputs are true. |
| `Or` | Returns true when either boolean input is true. |
| `Not` | Negates a boolean input. |
| `TernaryCondition` | Selects one of two typed values based on a boolean condition. |

## Comparison

Use comparison nodes to compare two values and produce boolean outputs.

| Display name | Purpose |
|---|---|
| `Equal` | Tests whether two values are equal. |
| `NotEqual` | Tests whether two values are not equal. |
| `Greater` | Tests whether the first value is greater than the second. |
| `GreaterOrEqual` | Tests whether the first value is greater than or equal to the second. |
| `Less` | Tests whether the first value is less than the second. |
| `LessOrEqual` | Tests whether the first value is less than or equal to the second. |

Agent notes:

- These nodes are typed. Bind the comparison type from schema, then validate compatibility.
- Use `If` when a comparison result should drive signal flow.

## Flow Control

Use flow control nodes to route signal or flow execution.

| Display name | Purpose |
|---|---|
| `Sequence` | Emits multiple output signals in order from one input signal. |
| `Switch` | Routes execution to a matching case output or default output. |
| `DoOnce` | Allows one signal through until reset. |
| `FlipFlop` | Alternates between two outputs on repeated triggers. |
| `Gate` | Opens, closes, or toggles whether signals can pass. |
| `If` | Routes a signal to true or false output based on a boolean condition. |
| `IfNull` | Routes a signal based on whether a value is null. |

## Type And Flow Adapters

Use adapter nodes when a graph needs to move between value-only and flow-style ports, or cast between types.

| Display name | Purpose |
|---|---|
| `ToFlow` | Converts a value into a flow payload. |
| `FromFlow` | Extracts a value from a flow payload and emits a signal. |
| `Cast` | Attempts to convert one typed value to another and routes success or failure. |

Agent notes:

- Prefer `suggest_adapter_nodes` before manually choosing adapters.
- Use `Cast` only when compatibility metadata or validation supports the conversion.

## Loops

Use loop nodes for repeated execution.

| Display name | Purpose |
|---|---|
| `ForEach` | Iterates through a collection, exposing current item and index. |
| `ForLoop` | Runs an index-based loop from first to last using a step value. |
| `WhileLoop` | Runs while a condition stays true. |

Agent notes:

- Connect loop body outputs carefully to avoid unexpected repeated side effects.
- Check item type compatibility for `ForEach` before connecting collection and item ports.

## Timing, Async, And Errors

Use these nodes for delayed execution, asynchronous work, and failure paths.

| Display name | Purpose |
|---|---|
| `Delay` | Delays flow for a configured duration. |
| `AsyncExecutor` | Executes asynchronous result-producing work and exposes the result. |
| `TryCatch` | Provides try, catch, and finally flow paths plus the caught exception value. |
| `Throw` | Throws an error from a provided error object or message. |
| `ThrowIfNull` | Throws when a value is null; otherwise passes through the non-null value. |

Agent notes:

- Treat `Throw`, `ThrowIfNull`, and `TryCatch` as control-flow-affecting nodes.
- Validate duration input type for `Delay` before setting values.

## Data And State

Use data nodes for state, buffers, delegates, logging, object mapping, property access, and null handling.

| Display name | Purpose |
|---|---|
| `Variable` | Stores a typed value and exposes the current value. |
| `Predicate` | Creates a reusable boolean condition from graph logic. |
| `Func` | Creates a reusable value-producing function from graph logic. |
| `Buffer` | Collects incoming values and emits a list when the buffer is ready. |
| `Logger` | Writes a configured log message for debugging or traceability. |
| `Mapper` | Builds an object from configured input members. |
| `Select` | Reads one configured property/member from an input object. |
| `SetProperty` | Updates one configured property/member on an object. |
| `NullCheck` | Produces booleans for null and not-null checks. |
| `NullValue` | Produces a null value of the selected type. |
| `NullCoalesce` | Uses fallback value when input is null. |
| `NullForgiving` | Treats a nullable value as non-null. Validate before using. |

Agent notes:

- Load `xtrader-nodes` before setting form data for `Mapper`, `Select`, `SetProperty`, or `Logger`.
- Do not invent property names. Inspect object type details or node form schema first.
- Prefer `NullCheck` plus `If` when null should control signal flow.

## Events

| Display name | Purpose |
|---|---|
| `Start` | Graph startup entry point. Use this to begin execution when the graph starts. |

## Selection Guide

| User intent | Start with |
|---|---|
| Expose a public visual-node input/output | IO / Public Port Nodes |
| Add, subtract, multiply, divide | Math |
| Combine boolean conditions | Logic |
| Route execution based on condition | `If` or `Switch` |
| Run multiple steps in order | `Sequence` |
| Loop over a collection | `ForEach` |
| Loop over indexes | `ForLoop` |
| Handle null values | Null utilities, `IfNull`, or `ThrowIfNull` |
| Build an object | `Mapper` |
| Read an object property/member | `Select` |
| Update an object property/member | `SetProperty` |
| Add debugging output | `Logger` |
| Start graph execution | `Start` |

## Search Guidance

When searching for Core nodes in the catalog:

- Search by capability and display name: `If`, `ForEach`, `Addition`, `Mapper`, `ValueInputPort`.
- Include `XTrader.Nodes.Core` as a package/source hint if search results are noisy.
- Treat returned MCP node details as authoritative for exact node code, ports, form data, and type params.
- For typed nodes, bind types from schema and validate the graph plan before applying.
