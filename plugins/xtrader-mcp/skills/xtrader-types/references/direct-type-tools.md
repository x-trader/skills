# Direct Type Tools

Use Direct MCP only when AgentReady v1 lacks the required type detail or mutation capability.

## Read / Inspect

| Tool | Use |
|---|---|
| `search_available_types` | Find project/package/system types |
| `get_type_details` | Inspect type schema/source |
| `get_type_form_schema` | Inspect value/form schema for a type |
| `check_type_compatibility` | Validate assignability between types |
| `suggest_type_for_port` | Find compatible type for a port |
| `analyze_type_usage` | Find graph/type references before mutation |
| `analyze_type_impact` | Classify safe/warning/breaking impact |

## Mutate

| Tool | Risk guidance |
|---|---|
| `create_object_type` | Validate property types first |
| `create_enum_type` | Verify exact enum values first |
| `create_type_from_json_sample` | Review inferred schema before saving |
| `update_type` | Analyze usage and impact first |
| `rename_type` | Analyze usage first |
| `move_type` | Low/medium risk; preserve references |
| `delete_type` | High risk; require confirmation |
