---
title: "Controlling ordering of NULL values in the ORDER BY clause"
datePublished: Wed Jun 05 2024 21:34:46 GMT+0000 (Coordinated Universal Time)
cuid: clx2ck23n000009jway3i06lg
slug: controlling-ordering-of-null-values-in-the-order-by-clause
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/IiEFmIXZWSw/upload/cf33eb2852f05f804cd38efaac49be0d.jpeg
tags: databases, google-cloud, sql, bigquery, data-engineering

---

Here's something I found out about the ORDER BY clause in BigQuery SQL the other day.

Check out the NULLS FIRST / NULLS LAST clauses. What do they do? They control how to treat NULL values when sorting.

While these are entirely optional, they're actually already happening behind the scenes even if you don't specify them.

🔹 ORDER BY \[column\] ASC (which is the default) uses NULLS FIRST if unspecified  
🔹 ORDER BY \[column\] DESC uses NULLS LAST if unspecified

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1717623214381/ff7df3d5-e17f-419b-a60c-129a17c87aa2.jpeg align="center")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://notjustsql.com)*.*