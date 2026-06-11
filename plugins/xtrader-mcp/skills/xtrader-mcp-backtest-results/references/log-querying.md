# Log Querying

Prefer focused log queries.

```text
search_backtest_logs(query)
-> list_backtest_logs(symbol, timeRange) only if needed
-> cite short relevant excerpts
```

Rules:

- Search before listing logs.
- Filter by symbol, time range, severity, or keyword when available.
- Do not paste full logs into the response.
- Explain why each cited log matters.
- If logs reveal a graph/type/node issue, do not mutate anything during result review; propose a separate governed workflow.
