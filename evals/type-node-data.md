# Eval: Type and Node Data

**Skills under test**: `xtrader-session`, `xtrader-catalog`, `xtrader-types`, `xtrader-nodes`, `xtrader-governance`, `xtrader-direct`

## Scenario

User asks: "Configure this generic mapper node to output a TradeSignal object and set its form fields. If the TradeSignal type does not exist, create it."

## Expected Agent Behavior

1. Start with AgentReady session context.
2. Load `xtrader-types` because type creation may be involved.
3. Load `xtrader-nodes` because generic params and form data may be involved.
4. Use catalog/compatibility tools first.
5. Explain Direct fallback if full node details or type creation is required.
6. Use `get_node_details` only on Direct MCP.
7. Verify required form fields and generic type param names before setting them.
8. Verify or create object type with explicit properties only.
9. Validate graph plan before apply.
10. Return to AgentReady after Direct fallback.

## Pass/Fail Rubric

| Criteria | Pass | Fail |
|---|---|---|
| Skill activation | Loads `xtrader-types` and `xtrader-nodes` | Continues with only catalog skill |
| Node details | Uses Direct fallback for `get_node_details` | Treats `get_node_details` as AgentReady |
| Object type | Verifies property names/types before create | Invents object schema |
| Enum handling | Verifies enum values before use | Invents enum values |
| Generic params | Reads param names from schema | Guesses type param names |
| Form data | Uses schema-provided form fields | Guesses form field names |
| Validation | Calls `validate_graph_plan` before apply | Applies without validation |
| Context | Returns to AgentReady after Direct fallback | Stays on Direct MCP |
| Inheritance | Does not assume inheritance unless MCP metadata returns it | Invents base type/inheritance |

## Negative Cases

| Case | Expected behavior |
|---|---|
| Agent creates `TradeSignal` with guessed properties | Fail — properties must be explicit or derived from MCP/user data |
| Agent sets `TOutput` without schema evidence | Fail — generic params must come from node schema |
| Agent calls `get_node_details` on AgentReady | Fail — use Direct fallback |
| Agent updates/deletes an existing type without impact analysis | Fail — must analyze usage/impact |
| Agent assumes `TradeSignal` inherits from another type | Fail unless MCP metadata says so |
