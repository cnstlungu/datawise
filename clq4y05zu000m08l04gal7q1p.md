---
title: "Approximate Aggregate Functions in BigQuery"
datePublished: Thu Dec 14 2023 08:32:46 GMT+0000 (Coordinated Universal Time)
cuid: clq4y05zu000m08l04gal7q1p
slug: approximate-aggregate-functions-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/rdbLJFv5odc/upload/137a4e9d4c07e048ad1f65bf8f80caa9.jpeg
tags: analytics, databases, google-cloud, sql, bigquery, data-engineering

---

Sometimes you don't need perfect, but just good enough. Take approximate aggregate functions in BigQuery, for example.

These are a type of aggregate functions that produce approximate results instead of exact ones but have the upside of typically requiring fewer resources for the computation.

When would I use one? This would be suitable where we can live with an uncertainty or small difference, especially for huge tables, during a preliminary check or data exploration.

Let's look at a practical example. Suppose we have the following data:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702542463705/e7d99e72-0e21-4933-9339-a8743d341b3a.png align="center")

`APPROX_TOP_COUNT` will compute the approx top N elements and their value counts

```sql
SELECT 
    APPROX_TOP_COUNT(value, 5) AS top_value_counts 
FROM `learning.data_source`
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702542553340/98f40f1b-5f07-42ac-a0ff-b26231ba61b6.png align="center")

`APPROX_COUNT_DISTINCT` will compute the approx distinct count (also can be grouped)

```sql
SELECT 
    APPROX_COUNT_DISTINCT(value) AS approx_distinct_value_count 
FROM `learning.data_source`
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702542629837/5e29d552-f166-4307-98e4-040a6fc27d8a.png align="center")

You can discover more approximate aggregate functions in the [documentation](https://cloud.google.com/bigquery/docs/reference/standard-sql/approximate_aggregate_functions).

Thanks for reading!

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*