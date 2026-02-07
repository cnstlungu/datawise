---
title: "Expressing multiple repeated joins as a correlated subquery"
seoTitle: "Optimize Joins with Correlated Subqueries"
seoDescription: "Discover how to use correlated subqueries in SQL to optimize multiple joins and improve query efficiency"
datePublished: Sun Feb 23 2025 15:13:22 GMT+0000 (Coordinated Universal Time)
cuid: cm7hrqlth000009jza1ni9im9
slug: expressing-multiple-repeated-joins-as-a-correlated-subquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/GsRaiFdcTY4/upload/53033ddb91c2a6155eb0ade4fda8c8d8.jpeg
tags: analytics, databases, google-cloud, sql, bigquery, gcp, data-engineering

---

In [yesterday’s post](https://datawise.dev/revisiting-group-by-rollup-with-a-more-realistic-example), we looked at retrieving information from a table by joining it multiple times—each with different join criteria. This raises a natural question: are there better alternatives to this approach?

I initially experimented with a CASE WHEN in the join condition, hoping it would short-circuit, picking the first matching condition—just like in a SELECT clause. However, in a join, it evaluates all scenarios, so that didn’t work as expected.

But remember correlated subqueries? A correlated subquery runs once per row and can be embedded in the SELECT or WHERE clause. Essentially, it lets you create a dynamic query within a single data cell, based on the current row’s context. Check out [this quick intro](https://datawise.dev/using-correlated-subqueries-in-bigquery).

To avoid multiple joins, you can use a correlated subquery to fetch all possible combinations (previously handled by join conditions) and apply the same logic with ORDER BY and LIMIT to return exactly one value.

A word of caution: correlated subqueries execute once per row, which can impact performance, especially with large datasets. However, they’re a valuable tool in your SQL tool belt, particularly when other elegant solutions aren’t available.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1740323268891/8607984d-3445-4040-bfab-d5b29cd62f6a.jpeg align="center")

*Found it useful? Subscribe to my Analytics newsletter at* [***notjustsql.com***](https://notjustsql.com/)*.*