---
title: "ORDER BY expressions in SQL"
datePublished: Mon Apr 01 2024 13:56:56 GMT+0000 (Coordinated Universal Time)
cuid: cluh0kwv9000a08ky5fwc0y7n
slug: order-by-expressions-in-sql
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/87hFrPk3V-s/upload/c27effb1cf78e2de3c3ea34c55832f86.jpeg
tags: analytics, databases, sql, bigquery, data-engineering

---

Friendly reminder: when you ORDER BY something in SQL, that something does not necessarily need to be a column, but could be an expression, the output of which can be ordered.

In the example below, we'd like to ORDER by sales decreasingly, but show the 'direct' sales first.

This is achieved by using a CASE WHEN that will rank direct sales above other types of sales, then sorting by the sales decreasingly.

![](https://miro.medium.com/v2/resize:fit:1164/0*V_Zc7tbY1A7spDyB align="left")

*Found it useful? Check out to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*