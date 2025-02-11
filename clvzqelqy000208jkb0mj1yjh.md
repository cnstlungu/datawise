---
title: "Order of precedence in SQL: WHERE vs HAVING"
datePublished: Thu May 09 2024 20:59:25 GMT+0000 (Coordinated Universal Time)
cuid: clvzqelqy000208jkb0mj1yjh
slug: order-of-precedence-in-sql-where-vs-having
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/cqvy_cag4gI/upload/7dce33787af01a107fddc6f9c612ad67.jpeg
tags: analytics, databases, google-cloud, sql, bigquery

---

If you're just getting started with SQL, this post is for you. So, it's worth looking at the order of precedence of SQL operators.

One particular case is WHERE vs HAVING, especially if you bind the aggregated column to the same column alias as in the input table.

This can save you from some unexpected results 😁

In short:  
\- WHERE = filter before aggregation  
\- HAVING = filter after aggregation

In the example below, the 'quantity' filtered in the HAVING clause is no longer the same 'quantity' in the original table, rather the SUM of quantities per each country bucket.

In practice, I'd rename the aggregated column to something like total\_quantity to make it more readable.

Depending what we need, we pick which approach we take, filtering out records before or after aggregation.

![](https://miro.medium.com/v2/resize:fit:1400/0*xjZr5hk5cnL6Dw-T align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](http://notjustsql.com)*.*