---
title: "Boolean data type in BigQuery"
datePublished: Wed Mar 27 2024 16:32:03 GMT+0000 (Coordinated Universal Time)
cuid: clua0x4pp000408jt91l8hnnu
slug: boolean-data-type-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/zj475haUy2M/upload/c9744b290c0a274cbd6430075640a2c4.jpeg
tags: analytics, google-cloud, sql, bigquery, data-engineering

---

I remember that one of the things that struck me some years ago when switching from SQL Server to BigQuery was the existence of the bool data type in the latter, which I didn't have before.

I still see from time to time BigQuery code that does not leverage it to the fullest.

For example, this means you can just say `val_b > val_a AS is_val_b_higher` for a boolean flag instead of comparing and determining TRUE/FALSE. Also, just `WHERE is_val_b_higher` instead of `WHERE is_val_b_higher IS/= TRUE`.

This, in my opinion, makes the query much more readable when working with boolean flags.

If you properly name the flags, reading the query feels much closer to natural language.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711557179992/1d5974d7-119f-435e-9ffa-c609688494b1.jpeg align="center")

*Found it useful? Check out to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*