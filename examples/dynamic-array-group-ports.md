# Example: Dynamic Array And Group Ports

**Endpoint**: `/mcp/agent-ready/v1`; use `/mcp` only when full node details or node-data mutation are unavailable through AgentReady.

**Skills**: `xtrader-session`, `xtrader-catalog`, `xtrader-types`, `xtrader-nodes`, `xtrader-visual-graphs`, `xtrader-graph-plan`, `xtrader-governance`, `xtrader-direct`

## Scenario

Configure a `MapperNode` with a `Slot` group containing `Name` and `Age`, then connect source values to `Slot.Name` and `Slot.Age`.

## Sequence

1. Load `xtrader-visual-graphs` to identify `group` behavior and dotted handles.
2. Load `xtrader-nodes` to inspect `MapperNode` schema and required form data/type params.
3. Load `xtrader-types` if output object type details are needed.
4. Configure `ArrayPorts["Slot"]` only if schema/handler requires dynamic member type definitions.
5. Set mapper form data from schema-backed `MapperNodeFormData` fields.
6. Connect source outputs to dotted target handles such as `Slot.Name` and `Slot.Age`.
7. Validate and repair before apply.

## Key Checks

- [ ] `MapperNode` uses a `group` input port named `Slot`.
- [ ] `SelectNode` is not treated as an array-port node; it has value input/output ports.
- [ ] Dotted handles are used only after schema confirms root port and member names.
- [ ] `ArrayPorts` maps dynamic root port names to `TypeDefine[]`, not edge IDs.
- [ ] Validation catches unknown dynamic ports and port-kind mismatches.
