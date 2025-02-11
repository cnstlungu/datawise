---
title: "Using LOGICAL_AND and LOGICAL_OR in BigQuery"
datePublished: Sun Dec 10 2023 00:24:38 GMT+0000 (Coordinated Universal Time)
cuid: clpyqt0sy000308iadnxv8608
slug: using-logicaland-and-logicalor-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/-SmCKTIcH5E/upload/6f3b03c5f83b1f16d17b271b1008445f.jpeg
tags: analytics, databases, google-cloud, sql, bigquery

---

Today I wanted to share another [BigQuery](https://www.linkedin.com/feed/hashtag/?keywords=bigquery) feature - maybe not the breathtaking - but definitely something to have in your toolbox. The occasion to use it might be around the corner.

So, have you ever encountered LOGICAL\_AND() and LOGICAL\_OR()? Think of them as aggregation functions but for boolean values. As the name implies:  
\- LOGICAL\_AND() returns True if all values as True  
\- LOGICAL\_OR() returns True if at least one value is True

A couple of things to know:  
\- It takes a boolean expression, but the boolean fields you use should not necessarily already be defined beforehand i.e. you can totally say: LOGICAL\_AND(status = 'ACTIVE')  
\- As with other aggregation functions you would need to use group by to compute results into bins

Let's look at a quick example of how it all works. Based on the data below, we'd like to find out whether all of a particular customer's orders were paid for and whether the customer has any outstanding amounts for any of his orders.

```sql
+-------------+----------+---------+--------------------+
| customer_id | order_id | is_paid | outstanding_amount |
+-------------+----------+---------+--------------------+
| 1           | 1001     | true    | 0                  |
| 1           | 1002     | true    | 0                  |
| 2           | 2001     | true    | 0                  |
| 2           | 2002     | false   | 100                |
| 3           | 3001     | false   | 150                |
| 3           | 3002     | false   | 250                |
+-------------+----------+---------+--------------------+
```

We're going to use `LOGICAL_AND` to assess if all of the orders are paid and `LOGICAL_OR` to check if at least one order has an outstanding amount greater than 0. We also need to group by `customer_id`.

```sql
SELECT 

    customer_id, 
    LOGICAL_AND(is_paid) AS all_orders_paid, 
    LOGICAL_OR(outstanding_amount > 0) AS has_outstanding_amounts 

FROM input_data

GROUP BY customer_id
```

Here's our output of our query.

```sql
+-------------+-----------------+-------------------------+
| customer_id | all_orders_paid | has_outstanding_amounts |
+-------------+-----------------+-------------------------+
| 1           | true            | false                   |
| 2           | false           | true                    |
| 3           | false           | true                    |
+-------------+-----------------+-------------------------+
```

Thanks for reading!

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*