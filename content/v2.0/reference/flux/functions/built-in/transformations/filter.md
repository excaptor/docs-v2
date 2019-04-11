---
title: filter() function
description: The `filter()` function filters data based on conditions defined in a predicate function (fn).
aliases:
  - /v2.0/reference/flux/functions/transformations/filter
menu:
  v2_0_ref:
    name: filter
    parent: built-in-transformations
weight: 401
---

The `filter()` function filters data based on conditions defined in a predicate function ([`fn`](#fn)).
The output tables have the same schema as the corresponding input tables.

_**Function type:** Transformation_  
_**Output data type:** Object_

```js
filter(fn: (r) => r._measurement == "cpu")
```

## Parameters

### fn
A single argument function that evaluates true or false.
Records are passed to the function.
Those that evaluate to true are included in the output tables.

_**Data type:** Function_

{{% note %}}
Objects evaluated in `fn` functions are represented by `r`, short for "record" or "row".
{{% /note %}}

## Examples
```js
from(bucket:"telegraf/autogen")
  |> range(start:-1h)
  |> filter(fn: (r) =>
    r._measurement == "cpu" and
    r._field == "usage_system" and
    r.cpu == "cpu-total"
  )
```

<hr style="margin-top:4rem"/>

##### Related InfluxQL functions and statements:
[SELECT](https://docs.influxdata.com/influxdb/latest/query_language/data_exploration/#the-basic-select-statement)