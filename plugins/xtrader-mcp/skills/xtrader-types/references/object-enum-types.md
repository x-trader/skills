# Object and Enum Types

## Object Types

Object types contain named properties. For each property, verify:

- property name
- property type
- required/optional state
- referenced project/package/system type availability

Use Direct fallback tools only when AgentReady lacks the needed capability:

- `search_available_types`
- `get_type_details`
- `create_object_type`
- `create_type_from_json_sample`
- `analyze_type_usage`
- `analyze_type_impact`
- `update_type`

## Enum Types

Enum types contain named values. Never invent enum values.

Before using or creating an enum, verify:

- enum name
- exact value names
- numeric/string values if present
- compatibility with consuming ports or form fields

Use Direct fallback tools only when needed:

- `get_type_details`
- `create_enum_type`
- `analyze_type_usage`
- `analyze_type_impact`

## Mutations

Before update/delete, use `analyze_type_usage` and `analyze_type_impact`. Treat `delete_type` as high risk and require governance.
