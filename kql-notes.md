## general kql notes

stats(values) in sql equivalent

```
TableName
| summarize item1_values = make_set(item1), count() by item2
```
