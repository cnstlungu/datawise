---
title: "Rolling period calculation in BigQuery"
datePublished: Wed Jan 17 2024 14:23:23 GMT+0000 (Coordinated Universal Time)
cuid: clrhvi1fr000309l2hsg9apg5
slug: rolling-period-calculation-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/08elrfBZ4A4/upload/b50daf19e0701a8fac083058d0126440.jpeg
tags: analytics, databases, google-cloud, sql, bigquery

---

How to compute a rolling period calculation in BigQuery?

In [one of my previous posts](https://datawise.dev/computing-a-cumulative-sum-in-bigquery), I've showcased using RANGE inside window function declarations in the context of computing a cumulative sum.

Today we're going to look at another example often found in the wild - computing a rolling period calculation. Let's look at an example.

We have customer order information and would like to compute a per customer rolling sum of the previous 60 days' worth of purchases.

How this would look in terms of SQL?

SUM(order\_total) OVER (PARTITION BY customer\_id ORDER BY UNIX\_DATE(order\_date) RANGE BETWEEN 59 PRECEDING AND CURRENT ROW) AS rolling\_60\_days\_sum

Let's explain it:

We will start by taking a SUM of order\_total with a window declaration  
and partitioning by customer\_id.

Next is ordering by our order\_date, but since RANGE only accepts a single integer field, we'll need to transform it using UNIX\_DATE. This will transform '2021-01-01' into 18628.

We can now use RANGE, setting the range between the 59 previous days and the current row. This way, if we have any gaps or duplicates in our order data (which is very likely), the calculation would still work, as opposed to the approach of using ROWS.

See below an illustration of how it all works.

```sql
SELECT 

customer_id, 
order_id, 
order_total, 
order_date, 
SUM(order_total) OVER (PARTITION BY customer_id
                       ORDER BY UNIX_DATE(order_date)
                       RANGE BETWEEN 59 PRECEDING AND CURRENT ROW) 
                 AS rolling_60_days_sum

FROM input_data


+-------------+----------+-------------+------------+---------------------+
| customer_id | order_id | order_total | order_date | rolling_60_days_sum |
+-------------+----------+-------------+------------+---------------------+
| Customer-1  | 10001    | 100         | 2021-01-01 | 100                 |
| Customer-1  | 10003    | 75          | 2021-02-15 | 175                 |
| Customer-1  | 10005    | 90          | 2021-03-12 | 165                 |
| Customer-1  | 10001    | 100         | 2021-04-21 | 190                 |
| Customer-1  | 10003    | 75          | 2021-05-12 | 175                 |
| Customer-1  | 10005    | 90          | 2021-06-23 | 165                 |
| Customer-2  | 10002    | 80          | 2021-01-01 | 80                  |
| Customer-2  | 10004    | 120         | 2021-02-04 | 200                 |
| Customer-2  | 10006    | 50          | 2021-03-05 | 170                 |
| Customer-2  | 10002    | 80          | 2021-04-11 | 130                 |
| Customer-2  | 10004    | 120         | 2021-05-12 | 200                 |
| Customer-2  | 10006    | 50          | 2021-06-30 | 170                 |
+-------------+----------+-------------+------------+---------------------+
```

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*