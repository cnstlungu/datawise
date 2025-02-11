---
title: "Filling up missing values with LAST_VALUE"
datePublished: Sun Dec 03 2023 16:35:13 GMT+0000 (Coordinated Universal Time)
cuid: clpppe8sc000809jw9jrven3d
slug: filling-up-missing-values-with-lastvalue
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/5B0IXL2wAQ0/upload/5f06fa587a04bdc5c5d0dc8b86ec3ec9.jpeg
tags: analytics, databases, sql, bigquery

---

Window functions are powerful. But they can also help us fill in missing data in BigQuery.

Let's say you have a sensor that records temperature and humidity. Unfortunately, it is quite unreliable, so sometimes it might not send one or both readings. You'd like to retain the last known reading for a measurement.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701621119948/b84aeea7-eed2-4c43-8b8d-e0c81c4abeec.png align="center")

Here's how we can solve it:

\- Leverage the LAST\_VALUE window function.  
\- Specify the IGNORE NULLS clause  
\- Partition by `sensor_id` so only we consider data from the same sensor  
\- Order the window by the timestamp column  
\- Define a ROWS condition to consider rows from the beginning of time up to and including the current row - this way, if we do have a current reading for this timestamp, we keep it.

Here's how it would look in SQL:

```sql
  SELECT


  sensor_id,
  temperature,
  humidity_percentage,
  at_timestamp,

  LAST_VALUE(temperature IGNORE NULLS) OVER (PARTITION BY sensor_id ORDER BY at_timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS tr_temperature,

  LAST_VALUE(humidity_percentage IGNORE NULLS) OVER (PARTITION BY sensor_id ORDER BY at_timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS tr_humidity,

FROM input_data

ORDER BY at_timestamp
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701621157497/81ec01b9-8293-4947-bb19-0332d18f77c4.png align="center")

Previously, I've written [another blog post solving a similar problem](https://hashnode.com/post/clfn1r5ys000b09l967kobbpe) by leveraging `NTH_VALUE` .

P.S. This would not work if you're trying to fill in a STRUCT for example. IGNORE NULLS does not regard STRUCT(NULL AS a, NULL AS b) the same as NULL, so you might need to unpack the STRUCT.

Happy querying!

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*