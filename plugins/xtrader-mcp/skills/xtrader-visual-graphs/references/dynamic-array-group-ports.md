# Dynamic Array And Group Ports

Array and group ports are dynamic schema concepts used by graph validation and code generation.

## ArrayPorts Mapping

Graph node data can include:

```text
Data.ArrayPorts: Dictionary<string, TypeDefine[]>
```

The dictionary key is the root dynamic port name. The array supplies member/slot types.

Example:

```text
ArrayPorts["Slot"] = [System.Decimal, System.Decimal]
```

This can allow dynamic handles such as:

```text
Slot.A
Slot.B
```

depending on node schema and handler behavior.

## ArrayPortSchema

`ArrayPortSchema` represents a collection-style port whose runtime members share an element type.

Validation checks:

- the `ArrayPorts` key names an existing array-compatible port;
- at least one type definition is supplied;
- connected slots have compatible types;
- array ports are not connected directly to value ports.

## GroupPortSchema

`GroupPortSchema` represents named typed value members.

Example handles:

```text
Slot.Name
Slot.Age
```

`MapperNode` uses a group input port named `Slot` and a value output port named `Output`.

Group validation checks:

- target group member exists;
- source/target member types are compatible;
- missing group members are reported as validation errors.

## SelectNode Correction

`SelectNode<TInput,TOutput>` does not use array ports. It has:

- `Input`: value input port
- `Output`: value output port

Use `SelectNode` to project one value into another value. Do not configure `ArrayPorts` for `SelectNode` unless its schema explicitly changes.

## Agent Rules

- Load `xtrader-nodes` before setting `ArrayPorts`.
- Use schema details or validation feedback to know whether the dynamic root is an array or group port.
- Use dotted handles only after confirming the root port and member names.
- Treat `ArrayPorts` as node data, not as graph edges.
