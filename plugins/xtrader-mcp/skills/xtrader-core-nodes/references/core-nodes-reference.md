# Core Nodes Reference

Core nodes are the building blocks of XTrader Visual Scripting. They are defined in `XTrader.Nodes.Core` and provide flow control, logic, math, data manipulation, and IO infrastructure for visual graphs.

Core nodes are **not** extracted from the .NET BCL. They have their own source-generated catalog via `[Node]` and `[Port]` attributes. Use this reference to understand what each node does and when to use it.

## IO / Port Infrastructure

Graph boundary nodes. Expose public ports on visual nodes for value, signal, and flow data.

| Node | Purpose |
|---|---|
| `ValueInputPortNode<T>` | Provide a typed value into a graph from outside. Outputs `Data`. |
| `ValueOutputPortNode<T>` | Expose a computed value outward. Inputs `Data`. |
| `SignalInputPortNode` | Accept a signal (no payload) into a graph. Outputs `Data`. |
| `SignalOutputPortNode` | Emit a signal outward. Inputs `Data`. |
| `FlowInputPortNode<T>` | Entry point for typed flow (trigger + payload) into a subgraph. |
| `FlowOutputPortNode<T>` | Exit point for typed flow from a subgraph. |

Port nodes add `Name` and `Description` input ports. Use these to create visual-node public ports.

## Math / Arithmetic

Generic over `INumber<T>`. Two numeric inputs (`A`, `B`), one output (`Result`).

| Node | Operation | Example |
|---|---|---|
| `AdditionNode<T>` | `A + B` | `3 + 5 = 8` |
| `SubtractionNode<T>` | `A - B` | `10 - 4 = 6` |
| `MultiplicationNode<T>` | `A * B` | `6 * 7 = 42` |
| `DivisionNode<T>` | `A / B` | `20 / 4 = 5` |

Search by display name: `Addition Int32`, `Subtraction Double`, etc.

## Logic

### Boolean

| Node | Operation |
|---|---|
| `AndNode` | `A && B` |
| `OrNode` | `A \|\| B` |
| `NotNode` | `!InputValue` |

### Ternary

| Node | Description |
|---|---|
| `TernaryConditionNode<T>` | `Condition ? True : False` — three inputs, one output of type `T`. |

### Comparison

Generic over `T`. Two inputs (`A`, `B`), two boolean outputs (`True`, `False`).

| Node | Operator |
|---|---|
| `EqualNode<T>` | `EqualityComparer<T>.Default.Equals(a, b)` |
| `NotEqualNode<T>` | `!Equals(a, b)` |
| `GreaterNode<T>` | `Compare(a, b) > 0` |
| `GreaterOrEqualNode<T>` | `Compare(a, b) >= 0` |
| `LessNode<T>` | `Compare(a, b) < 0` |
| `LessOrEqualNode<T>` | `Compare(a, b) <= 0` |

Search by display name: `Equal Int32`, `Greater String`, etc.

## Flow Control

### Branching

| Node | Description |
|---|---|
| `SequenceNode` | Triggers 4 output signals (`Then0`–`Then3`) in order on input. |
| `SwitchNode<T>` | Multi-way branch: matches `Selection` against `Case0`–`Case3`, emits matching `Out0`–`Out3` or `Default`. |
| `DoOnceNode` | Passes signal once until `Reset`. Has `StartClosed` option. |
| `FlipFlopNode` | Alternates between `A` and `B` outputs on each trigger. |
| `GateNode` | Allows/blocks signal based on `Open`/`Close`/`Toggle` state. |
| `IfNode` | Conditional: When signal + `Condition` bool → `True` or `False` signal. |
| `IfNullNode<T>` | Null-conditional: When signal + nullable `Data` → `IsNull` or `IsNotNull` signal. |

### Type Conversion

| Node | Description |
|---|---|
| `ToFlowNode<T>` | Converts a value into a flow (value in → flow out carrying the value). |
| `FromFlowNode<T>` | Extracts a value from a flow (flow in → `OnData` signal + `Data` value out). |

### Type Casting

| Node | Description |
|---|---|
| `CastNode<TIn, TOut>` | Attempts cast `TIn` → `TOut`. Emits `Success` or `Failure` signal + `Result` value. |

### Loops

| Node | Description |
|---|---|
| `ForEachNode<T>` | Iterates `IEnumerable<T>`: emits `Body` per-item, `Exit` after. Exposes `Item` and `Index`. |
| `ForLoopNode` | Index-based loop: `First`/`Last`/`Step` inputs, `Body` per-iteration, `Exit` after. Exposes `Index`. |
| `WhileLoopNode` | Conditional loop: emits `Body` while `Condition` is true, then `Completed`. |

### Timing

| Node | Description |
|---|---|
| `DelayNode` | Pauses flow for a `TimeSpan` duration (async `Task.Delay`). |

### Exceptions

| Node | Description |
|---|---|
| `TryCatchNode` | Try/Catch/Finally signal outputs + `Exception` value output. |
| `ThrowNode` | Throws exception from `Exception` or `Message` input. |
| `ThrowIfNullNode<T>` | Validates non-null, throws if null, otherwise passes signal + `Result`. |

### Async

| Node | Description |
|---|---|
| `AsyncExecutorNode<T>` | Executes a `Task<T>` (blocking `GetAwaiter().GetResult()`), outputs `Result`. |

## Data

### Variables

| Node | Description |
|---|---|
| `VariableNode<T>` | Stateful variable: stores value on signal, exposes current stored value. |
| `PredicateNode<T>` | Wraps a `Predicate<T>`: outputs a delegate that returns the `Result` input. |
| `FuncNode<TSource, TResult>` | Wraps a `Func<TSource,TResult>`: outputs a delegate that returns the `Result` input. |

### Collections

| Node | Description |
|---|---|
| `BufferNode<T>` | Buffers input values using Rx `Buffer(Count, Skip)`, outputs `List<T>` when buffer is ready. |

### Debug

| Node | Description |
|---|---|
| `LoggerNode<TSignal>` | Logs message via `ILogger`, with configurable `LogLevel` and `Key`. Uses JSON serialization. |

### Objects

| Node | Description |
|---|---|
| `MapperNode<TOutput, TSlotMembers>` | Constructs typed object from group port Slot members using bindings. |
| `SelectNode<TInput, TOutput>` | Projects input via selector function (e.g., `x.Property`). |
| `SetPropertyNode<TTarget, TValue>` | Sets a property on target object when signaled. Has In/Then flow ports. |

### Null Utilities

| Node | Description |
|---|---|
| `NullCheckNode<T>` | Outputs `IsNull`/`IsNotNull` booleans. |
| `NullValueNode<T>` | Provides a constant null value of type `T?`. |
| `NullCoalesceNode<T>` | Returns `Input ?? Fallback`. |
| `NullForgivingNode<T>` | Casts `T?` to `T` (null-forgiving `!` operator). |

## Events

| Node | Description |
|---|---|
| `OnStartNode` | Entry point: emits `OnStart` signal when graph starts. Implements `IStartupNode`. |

## Node Base Classes

| Base Class | Used By | Key Behavior |
|---|---|---|
| `FlowableNode` | `VariableNode`, `BufferNode`, `LoggerNode`, `ForEachNode`, `AsyncExecutorNode`, `ToFlowNode` | Adds `In`/`Then` signal ports, subscribes to `In`, calls abstract `OnSignal`. |
| `DataNode<T>` | `MapperNode`, `SelectNode`, `SetPropertyNode` | Generic constraint `where T : class`, for form-data-bearing nodes. |
| `PortNode` | All `*PortNode` | Adds `Name`/`Description` input ports for port-infrastructure nodes. |
| `ArithmeticNodeBase<T>` | `AdditionNode`, `SubtractionNode`, `MultiplicationNode`, `DivisionNode` | Adds `A`/`B` input ports, `Result` output port. |
| `ComparisonNodeBase<T>` | `EqualNode`, `NotEqualNode`, `GreaterNode`, `GreaterOrEqualNode`, `LessNode`, `LessOrEqualNode` | Adds `A`/`B` input ports, `True`/`False` boolean output ports. |

## Search Guidance

When searching for Core nodes in the catalog:
- Search by the `[Node("DisplayName")]` attribute name (e.g., `If`, `ForEach`, `Addition`, `Variable`)
- Core nodes live in the `XTrader.Nodes.Core` package
- They are excluded from .NET BCL extraction — do not search for them as `Create If` or `Add If`; they are found by their `Node` attribute name
- Generic nodes appear with their type parameters bound at search time (e.g., `Addition Int32`, `ForEach String`)
