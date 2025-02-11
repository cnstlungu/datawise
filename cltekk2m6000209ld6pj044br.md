---
title: "Using GROUP BY ALL in BigQuery"
datePublished: Tue Mar 05 2024 16:13:09 GMT+0000 (Coordinated Universal Time)
cuid: cltekk2m6000209ld6pj044br
slug: using-group-by-all-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/Vznty-DJTIk/upload/8e32176093bbd49812614e6a0fe0f31c.jpeg
tags: analytics, google-cloud, sql, bigquery, data-engineering

---

Featured in other database systems, the `GROUP BY ALL` has been [announced in preview](https://cloud.google.com/bigquery/docs/release-notes#February_26_2024) for BigQuery as well.

This will allow us to **not** enumerate all the non-aggregated columns when performing aggregates.

It's definitely better than `GROUP BY 1,2,3` which would fail once we'd change the list of columns we'd like to group by. Overall, I find it a useful shorthand when exploring or debugging.

Here's an example of how it looks.

```sql

SELECT country, sell_date, SUM(sales) AS total_sales

FROM input_data

-- new
GROUP BY ALL

-- instead of
-- GROUP BY country, sell_date
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1709655123449/33f5b5a0-a6e5-40a6-be63-e7217d07dbf7.png align="center")

*Found it useful? Check out to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*