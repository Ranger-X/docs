---
editable: false
sourcePath: en/_api-ref/datalens/function-ref/RAVG.md
---


# RAVG (window)



#### Syntax {#syntax}


```
RAVG( value [ , direction ] [ TOTAL | WITHIN ... | AMONG ... ] [ ORDER BY ... ] [ BEFORE FILTER BY ... ] )
```

#### Description {#description}

{% note warning %}

The sorting order is based on the fields listed in the sorting section of the chart and in the `ORDER BY` clause. First, `ORDER BY` fields are used, and then they are complemented by the fields from the chart.

{% endnote %}

Returns the average of all values in a growing (or shrinking) window defined by the sort order and the value of `direction`:

| `direction`   | Window                                                 |
|:--------------|:-------------------------------------------------------|
| `"asc"`       | Starts from the first row and ends at the current row. |
| `"desc"`      | Starts from the current row and ends at the last row.  |

By default `"asc"` is used.


Window functions with a similar behavior: [RSUM](RSUM.md), [RCOUNT](RCOUNT.md), [RMIN](RMIN.md), [RMAX](RMAX.md).

See also [AVG](AVG.md), [MAVG](MAVG.md).

**Argument types:**
- `value` — `Fractional number | Integer`
- `direction` — `String`


**Return type**: `Integer`

{% note info %}

Only constant values are accepted for arguments (`direction`).

{% endnote %}


#### Examples {#examples}

```
RAVG([Profit])
```

```
RAVG([Profit], "asc")
```

```
RAVG([Profit] TOTAL)
```

```
RAVG([Profit], "desc" WITHIN [Date])
```

```
RAVG([Profit] AMONG [Date])
```


#### Data source support {#data-source-support}

`Materialized Dataset`, `ClickHouse 19.13`, `Microsoft SQL Server 2017 (14.0)`, `MySQL 5.6`, `Oracle Database 12c (12.1)`, `PostgreSQL 9.3`.
