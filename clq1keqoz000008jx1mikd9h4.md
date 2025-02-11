---
title: "Using ANY_VALUE()  in BigQUERY"
datePublished: Mon Dec 11 2023 23:48:53 GMT+0000 (Coordinated Universal Time)
cuid: clq1keqoz000008jx1mikd9h4
slug: using-anyvalue-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/uKlneQRwaxY/upload/b35059adc4cce2810f840107f05c5221.jpeg
tags: analytics, databases, google-cloud, sql, bigquery, data-engineering

---

Have you ever used ANY\_VALUE in BigQuery?

It's an aggregate function like SUM or AVG, but it returns a non-deterministic (not random) row from the group. I've been using it in scenarios where there's one value anyway, such as when PIVOTing.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702338281074/788060a1-25a1-4aeb-9df8-b5b19f518de8.png align="center")

```sql
WITH input_data AS (
  SELECT 'Europe' AS Region, 'Q1' AS quarter, 250000 AS sales
  UNION ALL
  SELECT 'Europe' AS Region, 'Q2' AS quarter, 225000 AS sales
  UNION ALL
  SELECT 'Europe' AS Region, 'Q3' AS quarter, 275000 AS sales
  UNION ALL
  SELECT 'Europe' AS Region, 'Q4' AS quarter, 290000 AS sales
  UNION ALL
  SELECT 'MEA' AS Region, 'Q1' AS quarter, 190000 AS sales
  UNION ALL
  SELECT 'MEA' AS Region, 'Q2' AS quarter, 210000 AS sales
  UNION ALL
  SELECT 'MEA' AS Region, 'Q3' AS quarter, 300000 AS sales
  UNION ALL
  SELECT 'MEA' AS Region, 'Q4' AS quarter, 220000 AS sales
)

SELECT * FROM input_data

PIVOT(ANY_VALUE(sales) as sales FOR quarter IN ('Q1', 'Q2', 'Q3', 'Q4'));
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702338300651/6dbc23cf-399c-41d0-a2da-38148a96d4c1.png align="center")

Upon documenting myself for this post, I found an interesting thing - it supports the HAVING clause, allowing us to restrict the rows this function is aggregating, either by a MIN or MAX of a given expression.

Let's look at how it works. Say we have the following data:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702338367365/31e6905a-11ba-4325-8efe-baabf95d2d37.png align="center")

We're going to compute the product that has sold the highest by value and the product that has sold the least by quantity in each of the countries.

```sql
WITH input_data AS (
  SELECT 'Germany' AS country, 'productA' AS product_id, 200 AS quantity, 5.00 AS price
  UNION ALL
    SELECT 'Germany' AS country, 'productB' AS product_id, 75 AS quantity, 100.00 AS price
  UNION ALL
    SELECT 'Germany' AS country, 'productC' AS product_id, 100 AS quantity, 120.00 AS price
  UNION ALL
    SELECT 'Spain' AS country, 'productA' AS product_id, 300 AS quantity, 5.00 AS price
  UNION ALL
    SELECT 'Spain' AS country, 'productD' AS product_id, 250 AS quantity, 20.00 AS price
  UNION ALL
    SELECT 'Spain' AS country, 'productE' AS product_id, 100 AS quantity, 15.00 AS price
)

SELECT 
    country, 
    ANY_VALUE(product_id HAVING MAX quantity*price) AS highest_selling_by_value,
    ANY_VALUE(product_id HAVING MIN quantity) AS lowest_selling_by_quantity,
FROM input_data
GROUP BY country
```

Here's what the results would look like:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702338470054/cdda5706-963f-461a-881c-9e279db22998.png align="center")

Thanks for reading!

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*