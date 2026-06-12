# Port Node Patterns

Public ports of a project visual node come from official internal port nodes in the graph.

## Official Public Port Nodes

```text
XTrader.Nodes.Core.IO.ValueInputPort
XTrader.Nodes.Core.IO.ValueOutputPort
XTrader.Nodes.Core.IO.SignalInputPort
XTrader.Nodes.Core.IO.SignalOutputPort
XTrader.Nodes.Core.IO.FlowInputPort
XTrader.Nodes.Core.IO.FlowOutputPort
```

Only these official types are recognized as public visual-node port nodes.

## Shared Fields

Every public port node needs:

```text
InputPortsValues["Name"] = "PublicPortName"
```

Optional:

```text
InputPortsValues["Description"] = "Human-readable description"
```

## Value Port Nodes

Value input/output port nodes require:

```text
TypeParams["T"] = TypeDefine(...)
```

They produce external `ValuePortSchema` ports.

## Flow Port Nodes

Flow input/output port nodes require:

```text
TypeParams["T"] = TypeDefine(...)
```

They produce external `FlowPortSchema` ports.

## Signal Port Nodes

Signal input/output port nodes do not carry a value type and do not need `TypeParams["T"]`.

They produce external `SignalPortSchema` ports.

## Agent Rules

- Use `xtrader-catalog` to locate the exact port node codes.
- Use `xtrader-nodes` before setting `InputPortsValues` or `TypeParams`.
- Use `xtrader-graph-plan` to add port nodes and validate the graph.
- Do not create public array/group ports through guessed port-node names; no dedicated public group/array port nodes exist yet.
