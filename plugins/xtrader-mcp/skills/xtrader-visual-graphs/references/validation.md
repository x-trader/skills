# Visual Graph Validation

Visual graph validation protects graph shape, schema compatibility, and compile-time correctness.

## Node Validation

Validation checks:

- required user-provided type params exist;
- input values target known input ports;
- literal input values are compatible with expected types;
- array port mappings target known array/group dynamic ports;
- array port mappings include at least one type definition;
- required form data fields exist.

## Edge Validation

Validation checks:

- source node exists;
- target node exists;
- source handle exists on source output ports;
- target handle exists on target input ports;
- source and target port kinds match;
- value/flow/array/group member types are compatible;
- group members referenced by dotted handles exist.

## Common Errors

| Error pattern | Fix |
|---|---|
| `source_port_not_found` | Inspect source node output schema and use exact handle. |
| `target_port_not_found` | Inspect target node input schema and use exact handle. |
| `port_kind_mismatch` | Connect matching kinds only. |
| `incompatible_types` | Choose adapter node, compatible type, or correct type param. |
| `missing_required_type_parameter` | Set required `TypeParams`. |
| `unknown_dynamic_port` | Set `ArrayPorts` only on array/group schema ports. |
| `missing_required_form_field` | Set schema-required `FormData` fields. |

## Agent Rules

- Treat validation output as source of truth.
- Repair plans and validate again before apply.
- Do not ignore warnings about unknown input values or unusual signal values.
