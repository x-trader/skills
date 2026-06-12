# Port Kinds

XTrader graph validation distinguishes port kind and type compatibility.

## Value

`value` ports carry one typed data value.

Examples:

- `IInputValuePort<T>`
- `IOutputValuePort<T>`
- `ValuePortSchema`

Use value ports for data dependencies such as `price`, `symbol`, `TradeSignal`, `Candle`, or `Person`.

Connection rule: output value to input value with compatible type.

## Signal

`signal` ports carry control flow only. They have no value payload.

Examples:

- `SignalPortSchema`
- flowable `In` / `Then` style control ports

Use signal ports to sequence execution where no data travels with the trigger.

Connection rule: output signal to input signal only.

## Flow

`flow` ports carry both execution trigger and a typed payload. Conceptually: signal plus data.

Examples:

- `IInputFlowPort<T>`
- `IOutputFlowPort<T>`
- `FlowPortSchema`

Use flow ports when ordering and a value must travel together.

Connection rule: output flow to input flow with compatible payload type.

## Array

`array` ports represent dynamic collection-style members with configured element/member types.

Examples:

- `ArrayPortSchema`
- graph node `Data.ArrayPorts[portName] = TypeDefine[]`

Use array ports when a node supports a variable number of typed slots.

Connection rule: array to array with compatible element/slot types. Do not connect array directly to value.

## Group

`group` ports are named sets of typed value members.

Examples:

- `GroupPortSchema`
- `MapperNode.Slot`
- handles like `Slot.Name` or `Slot.Age`

Use group ports when a node consumes or produces structured named values.

Connection rule: connect compatible group members by dotted handles, or group to group when member names and types are compatible.
