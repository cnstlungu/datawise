---
title: "Using ARRAY_AGG in BigQuery"
datePublished: Tue Nov 07 2023 22:46:08 GMT+0000 (Coordinated Universal Time)
cuid: cloox73ny000308jn85ee6x4c
slug: using-array-agg-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/ZzApzgh5lxo/upload/156c530d9ce565177d1e25f446e485e2.jpeg
tags: analytics, databases, sql, bigquery

---

Almost everybody knows the usual standard SQL aggregation functions like SUM, MAX or AVG. In this short post, we're going to look at ARRAY\_AGG: another useful aggregation function.

So, what does it do?

ARRAY\_AGG allows us to aggregate multiple rows into a single array, based on a particular grouping. It's quite useful when modeling one-to-many relationships, like customers and orders.

For example, let's analyze the following input table.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699396326502/f129b137-f9af-401f-95a2-4b5f720e9301.png align="center")

Let's say we'd like to aggregate the order data into an ARRAY of STRUCTs, grouped by customer\_id. Let's also order the resulting array decreasingly by the order\_total .

The code to do that would look as follows:

```sql

SELECT 

  customer_id, 
  ARRAY_AGG( STRUCT(order_id, order_total ) ORDER BY order_total DESC) AS order_details

FROM input_data

GROUP BY customer_id
```

Here's how the processed data looks like:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699396878896/f785d1f3-512e-4b49-aa08-3df7d396931d.png align="center")

We can now see that instead of the 6 initial rows, we have 2 rows - 1 per customer\_id and an array of STRUCTS with order details.

Note that ARRAY\_AGG can be combined with:  
\- DISTINCT, to eliminate duplicates in the resulting ARRAY  
\- STRUCT, to create an ARRAY of STRUCTS  
\- ORDER BY, to order the ARRAY in a particular way  
\- LIMIT, to keep only first n entries (based on the ordering)

Thanks for reading!

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*