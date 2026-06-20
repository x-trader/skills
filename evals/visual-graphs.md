# Eval: Visual Graphs

**Skills under test**: `xtrader-session`, `xtrader-catalog`, `xtrader-core-nodes`, `xtrader-nodes`, `xtrader-visual-graphs`, `xtrader-graph-plan`, `xtrader-governance`, `xtrader-direct`

## Scenario

User asks: "Create a reusable visual node with a decimal Price input and a boolean Accepted output, then use it inside another graph. Also explain whether SelectNode needs ArrayPorts."

## Expected Agent Behavior

1. Starts with AgentReady session context.
2. Loads `xtrader-visual-graphs` because VisualNode/FlowGraph composition is involved.
3. Uses official `ValueInputPort` and `ValueOutputPort` nodes for public ports.
4. Sets port `Name` via `InputPortsValues["Name"]`.
5. Sets value port type through `TypeParams["T"]`.
6. Explains that the created visual node can be nested as a normal graph node after its schema is available.
7. Uses catalog/node details before connecting handles.
8. Explains that `SelectNode` has value input/output ports, not array ports.
9. Validates graph plan before apply.

## Pass/Fail Rubric

| Criteria | Pass | Fail |
|---|---|---|
| Skill activation | Loads `xtrader-visual-graphs` | Uses only graph-plan guidance |
| Public ports | Uses official Core IO public port nodes | Invents external schema ports |
| Value ports | Sets `TypeParams["T"]` | Leaves type params guessed/missing |
| Composition | Treats visual node as reusable/nestable after schema exists | Says visual nodes cannot be nested |
| SelectNode | Says SelectNode uses value ports | Claims SelectNode needs ArrayPorts |
| Validation | Validates before apply | Applies without validation |

## Negative Cases

| Case | Expected behavior |
|---|---|
| Agent creates a guessed group public-port node | Fail; no dedicated public group/array port nodes yet |
| Agent connects `array` to `value` | Fail; port kind mismatch |
| Agent uses dotted handle without schema evidence | Fail; must inspect schema/validation |
| Agent sets `ArrayPorts` on SelectNode | Fail unless schema explicitly requires it |
