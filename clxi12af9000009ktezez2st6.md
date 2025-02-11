---
title: "Self-joins in SQL"
datePublished: Sun Jun 16 2024 20:57:20 GMT+0000 (Coordinated Universal Time)
cuid: clxi12af9000009ktezez2st6
slug: self-joins-in-sql
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/betmVWGYcLY/upload/206a37909373c7878881a470d9948bb6.jpeg
tags: databases, google-cloud, sql, bigquery, data-engineering

---

Let's talk about self-joins in SQL. It's one of the join types that don't have their own keyword, but is more of a concept.

It essentially means you are joining a table with itself to retrieve some result from another row.

Prior to the introduction of window functions, self-joins were much more prevalent - you would, for example, join the table to itself to retrieve the value for the previous day.

When considering using a self-join, be mindful of the performance implications. BigQuery, for example, [explicitly lists self-joins as an anti-pattern](https://cloud.google.com/bigquery/docs/best-practices-performance-compute#avoid_self_joins). That is not to say that the need for self-tables has disappeared, there are still cases where we'd need it.

Let's look at an example. We have a table containing all the employee data, including the id of their manager.

If order to retrieve their manager's name, we'd need to perform a self join, using manager\_id in the join condition.

By the way, this particular case can also be solved with a [recursive common-table expression](https://datawise.dev/recursive-ctes-in-bigquery).

![](https://miro.medium.com/v2/resize:fit:1400/0*dcNBdqa93vnwjwPV align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://notjustsql.com)*.*