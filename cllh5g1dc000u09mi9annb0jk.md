---
title: "Using ROLLUP in BigQuery"
datePublished: Fri Aug 18 2023 22:15:46 GMT+0000 (Coordinated Universal Time)
cuid: cllh5g1dc000u09mi9annb0jk
slug: using-rollup-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/Wpnoqo2plFA/upload/8ba42636e1c671d4a2e77ec7ee1c19fd.jpeg
tags: analytics, sql, bigquery

---

Today's short post is about using the [#ROLLUP](https://www.linkedin.com/feed/hashtag/?keywords=rollup&highlightedUpdateUrns=urn%3Ali%3Aactivity%3A7098295702987927552) command in [#BigQuery](https://www.linkedin.com/feed/hashtag/?keywords=bigquery&highlightedUpdateUrns=urn%3Ali%3Aactivity%3A7098295702987927552)[#SQL](https://www.linkedin.com/feed/hashtag/?keywords=sql&highlightedUpdateUrns=urn%3Ali%3Aactivity%3A7098295702987927552). Funnily enough, I haven't encountered it until recently, and not yet in the wild anyway. That doesn't mean it's not useful though.

🔍 What is ROLLUP? The ROLLUP function provides a way to do hierarchical aggregation in SQL. It allows us to create subtotals and grand totals in one query, rather than multiple queries.

Imagine you're grouping by several columns a,b, and c to compute an aggregate. GROUP BY ROLLUP(a,b,c) will perform an aggregation across the following sets:  
\-(a, b, c)  
\-(a, b)  
\-(a)  
\-()

🌟 Let's see an example:  
Consider a sales table with columns Region, Product, and SalesAmount.

A standard GROUP BY might look like this:

```sql
SELECT Product, Region, SUM(SalesAmount) as total_sales
FROM sales
GROUP BY Product, Region;
```

This would produce a sum of Sales Amount per each product-region combination.

```sql
+------------+--------+-------------+
| Product    | Region | total_sales |
+------------+--------+-------------+
| Headphones | Europe | 100         |
| Keyboard   | Europe | 150         |
| Webcam     | Europe | 200         |
| Headphones | Asia   | 200         |
| Keyboard   | Asia   | 300         |
| Webcam     | Asia   | 400         |
+------------+--------+-------------+
```

At the same time, including ROLLUP would look like:

```sql
SELECT Region, Product, SUM(SalesAmount)
FROM sales
GROUP BY ROLLUP (Region, Product)
```

This would produce a sum of Sales Amount per each product-region combination as well, but also a row for each Region's sub-total and a grant total row for all regions.

```sql
+--------+------------+-------------+
| Region | Product    | total_sales |
+--------+------------+-------------+
|        |            | 1350        |
| Europe |            | 450         |
| Europe | Headphones | 100         |
| Europe | Keyboard   | 150         |
| Europe | Webcam     | 200         |
| Asia   |            | 900         |
| Asia   | Headphones | 200         |
| Asia   | Keyboard   | 300         |
| Asia   | Webcam     | 400         |
+--------+------------+-------------+
```

⚠ The order of columns in the ROLLUP matters.  
ROLLUP BY (Product, Region) would produce sub-totals by Product instead of subtotals by Region.

```sql
+------------+--------+-------------+
| Product    | Region | total_sales |
+------------+--------+-------------+
|            |        | 1350        |
| Headphones |        | 300         |
| Headphones | Europe | 100         |
| Keyboard   |        | 450         |
| Keyboard   | Europe | 150         |
| Webcam     |        | 600         |
| Webcam     | Europe | 200         |
| Headphones | Asia   | 200         |
| Keyboard   | Asia   | 300         |
| Webcam     | Asia   | 400         |
+------------+--------+-------------+
```

Thanks for reading and keep discovering BigQuery!

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*