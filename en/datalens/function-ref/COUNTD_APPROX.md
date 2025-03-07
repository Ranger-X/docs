---
editable: false
sourcePath: en/_api-ref/datalens/function-ref/COUNTD_APPROX.md
---


# COUNTD_APPROX



#### Syntax {#syntax}


```
COUNTD_APPROX( value )
```

#### Description {#description}
Returns the approximate number of unique values in the group. Faster than [COUNTD](COUNTD.md), but doesn't guarantee accuracy.

**Argument types:**
- `value` — `Any`


**Return type**: `Integer`

#### Example {#examples}

```
COUNTD_APPROX([ClienID])
```


#### Data source support {#data-source-support}

`Materialized Dataset`, `ClickHouse 19.13`, `Oracle Database 12c (12.1)`, `YDB`.
