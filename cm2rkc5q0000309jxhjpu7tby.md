---
title: "Not all NULLS are the same"
datePublished: Sun Oct 27 2024 12:25:21 GMT+0000 (Coordinated Universal Time)
cuid: cm2rkc5q0000309jxhjpu7tby
slug: not-all-nulls-are-the-same
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/5B0IXL2wAQ0/upload/d5a7ab49550c9e19dd49803598e2b5e5.jpeg
tags: databases, google-cloud, sql, bigquery, data-analytics

---

So NULLs are definitely beasts of their own and as Data Engineers we come to learn to take them into account.

That is because not knowing their quirks can lead to unexpected results or errors. Let's look at how not all NULLS are the same in BigQuery SQL.

First, sure, the NULL means the absence of a value, but it is bound to a particular data type (so it's like "i'm a missing an INT64 here"). It can be found in columns with the NULLABLE mode, therefore a DATETIME NULL and a NUMERIC NULL cannot be compared as they are different types.

I've also seen that if we specify just the NULL literal, it defaults to INTEGER.

![](https://miro.medium.com/v2/resize:fit:1400/0*7XVYCmbQG_Q_vZqA align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [https://www.notjustsql.com](https://www.notjustsql.com/)*.*