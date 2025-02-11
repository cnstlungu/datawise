---
title: "Comparing ranking functions in BigQuery"
datePublished: Wed Nov 15 2023 21:59:31 GMT+0000 (Coordinated Universal Time)
cuid: clp0b1yti00000ajtflzj29k1
slug: comparing-ranking-functions-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/NfLZeAN7I6s/upload/86d1c04aabb5592ed41127daf364c2f6.jpeg
tags: analytics, databases, sql, bigquery

---

One of the most common sightings in SQL code is using ranking functions. It's simple but we must surely get it right. I use `ROW_NUMBER` very often for de-duplication, also used `DENSE_RANK` a couple of times - but I've never used `RANK`. So how are they different?

\- ROW\_NUMBER - sequential row number, regardless of equal values. If no order is provided, the results might be different every time you run it (aka non-deterministic): 1,2,3,4,5

\- DENSE\_RANK - also a sequential row number, but takes into account peer rows (with equal values). next rank is the immediate following: 1,2,2,3 (no gaps)

\- RANK - also a sequential row number, takes into account rows with equal values, but next rank is incremented: 1,2,2,4 (with gaps)

See below for an example of how it all works.

```sql
SELECT 
  store_code, 
  country, 
  sales_usd, 
  ROW_NUMBER() OVER country_sales AS row_no,
  DENSE_RANK() OVER country_sales AS dense_rnk,
  RANK() OVER country_sales       AS rnk

FROM input_data

WINDOW country_sales AS (PARTITION BY country ORDER BY sales_usd DESC)
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700085468660/b8adf7bc-2986-415b-9021-27dea095e082.png align="center")

Thanks for reading!

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*