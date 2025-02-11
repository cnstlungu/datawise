---
title: "Concatenation operator in BigQuery"
datePublished: Sun Apr 28 2024 21:43:07 GMT+0000 (Coordinated Universal Time)
cuid: clvk24eul000c0aifc0j911h6
slug: concatenation-operator-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/BARpgWJDSIA/upload/7daddeb83e4c753acce28c2174fb48be.jpeg
tags: analytics, databases, google-cloud, sql, bigquery

---

You might have encountered the slightly odd-looking `||` in SQL before, whether in BigQuery or your other database system.

If not yet, it's called the 'concatenation operator' and well, it concatenates things.

In fact, it's the ANSI SQL standard concatenation operator so in theory it should work across database engines (but it doesn't - for example SQL Server uses `+` instead for concatenating strings).

In BigQuery, it does the same thing as `CONCAT()` for STRINGs and `ARRAY_CONCAT()` for ARRAYs .

![](https://miro.medium.com/v2/resize:fit:1400/0*4CFhRtK_01ljuPKD align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*