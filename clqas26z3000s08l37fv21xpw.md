---
title: "Using COUNTIF() in BigQuery"
datePublished: Mon Dec 18 2023 10:33:00 GMT+0000 (Coordinated Universal Time)
cuid: clqas26z3000s08l37fv21xpw
slug: using-countif-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/gdL-UZfnD3I/upload/21ecd3400789d32440f8cdc15de6b2b1.jpeg
tags: analytics, databases, google-cloud, sql, bigquery, data-engineering

---

Happy weekend! Do you remember the good old COUNTIF from Excel?  
When I was just starting out in Analytics and was working with spreadsheets, I would make heavy use of it.

Well, turns out we have something similar in BigQuery as well.

It's an aggregate function, counting only rows that fulfill a given condition, for example `COUNTIF( a > 10 and b = 'text')`

Of course, this would be pretty much the same as combining COUNT + CASE WHEN.

See a quick example below.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702895485510/cc4722bc-364d-4afb-b040-8195e4b65442.jpeg align="center")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*