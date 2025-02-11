---
title: "Watch out when using SAFE_CAST in BigQuery"
datePublished: Fri Feb 16 2024 14:59:06 GMT+0000 (Coordinated Universal Time)
cuid: clsorzj3300030akzcwr68rbj
slug: watch-out-when-using-safecast-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/Hf7x860ktHc/upload/0bf7ef4cd9b6a191e8ebc88443310215.jpeg
tags: analytics, databases, sql, bigquery, dataengineering

---

Here's an interesting situation I've seen with BigQuery.

Say a source system provides JSON events with timestamps at microsecond grain (6 decimals, so something like `2024-01-01 14:00:00.123456`).

This is cast using SAFE\_CAST into a proper TIMESTAMP. All works just fine.

Until one day the source system sends the JSON with timestamps at NANOsecond grain.  
Since timestamp has only MICROsecond precision, the cast quietly fails (no error), a null is returned from a seemingly correct looking timestamp.

Without proper monitoring this issue can go unnoticed quite a bit. So watch out 🤔

It just drives the point home on how important is to have proper monitoring in place and enforcing a robust data contract with data sources.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708095414281/fb407b2e-5d5c-400a-93b1-fe1fe9ba278a.jpeg align="center")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*