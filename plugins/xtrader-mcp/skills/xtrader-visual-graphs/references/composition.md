# Visual Node Composition

A project visual node can be used inside another visual node graph.

## How It Works

1. Create or locate a visual node.
2. Ensure its internal graph exposes public ports through official port nodes.
3. Save and validate the visual node graph.
4. Search catalog/project nodes for the visual node.
5. Add it as a graph node instance in another visual node graph.
6. Connect to its generated external ports.

The outer graph sees the visual node through the schema produced from its internal public port nodes.

## Example Shape

```text
Inner visual node: PriceFilter
  internal graph:
    ValueInputPort(Name="Price", T=System.Decimal)
    ValueOutputPort(Name="Accepted", T=System.Boolean)

Outer visual node:
  nodes:
    candle-source
    price-filter-instance (Type = project node code for PriceFilter)
    notify
  edges:
    candle-source.Price -> price-filter-instance.Price
    price-filter-instance.Accepted -> notify.Condition
```

## Agent Rules

- Do not assume a visual node is available in catalog immediately after creation unless session/context is refreshed.
- Check the visual node's generated/public schema before connecting to it.
- Use `xtrader-graph-plan` for add/connect operations.
- Use `xtrader-governance` before applying graph changes.
