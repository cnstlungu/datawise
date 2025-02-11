---
title: "Here's how GROUP BY works differently across SQL dialects"
datePublished: Sat Jun 08 2024 16:36:18 GMT+0000 (Coordinated Universal Time)
cuid: clx6c7s4f00000ala50hmfh0y
slug: heres-how-group-by-works-differently-across-sql-dialects
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/EA4MvInOSy0/upload/9a8183667a253bd19f06a5e2676cd65a.jpeg
tags: sql-server, databases, google-cloud, sql, bigquery

---

It turns out I've been writing longer queries than I should.😁 Here's an interesting gotcha about GROUP BY between SQL dialects that I've just learned.

So I've started with SQL Server back in the day, where according to docs:

> a GROUP BY column expression cannot be "a column alias that is defined in the SELECT list".

Naturally, if I processed a column during aggregation, I would have the same expression in GROUP BY (minus the alias of course).

```sql
SELECT 
CASE WHEN country in ('US','USA','US of A') THEN 'USA' ELSE country END AS country, SUM (sales_amount) AS total_sales
FROM sales
GROUP BY CASE WHEN country in ('US','USA','US of A') THEN 'USA' ELSE country END
```

Where it matters: if the alias is the same as the original column name, you would be grouping not by the 'transformed' column, but by the original one, yielding things you might not expect 😁 A newly-assigned alias cannot be grouped by for the same reason.

Well, things are different with BigQuery for instance. Docs mention:

> GROUP BY clauses may also refer to aliases. If a query contains aliases in the SELECT clause, those aliases override names in the corresponding FROM clause.

So in BQ, you can reference the alias you've assigned in SELECT (overriding the one from FROM if matching) and you can reference a newly aliased column. No need to copy the unwieldy `CASE WHEN ...` to the `GROUP BY` in this case.

```sql
SELECT 
 country AS cntry,
 SUM(amount) AS total_amount
FROM input_data
GROUP BY cntry
```

Lesson learned (for now).

![](https://miro.medium.com/v2/resize:fit:1400/0*PLT2zB3ECkvWehgh align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://notjustsql.com)*.*