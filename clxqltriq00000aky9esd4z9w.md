---
title: "LAX JSON conversion functions in BigQuery"
datePublished: Sat Jun 22 2024 21:00:44 GMT+0000 (Coordinated Universal Time)
cuid: clxqltriq00000aky9esd4z9w
slug: lax-json-conversion-functions-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/cGH4jzeam0E/upload/587a432ae4b3e2e33ebbacf1635996bd.jpeg
tags: databases, google-cloud, sql, bigquery, data-engineering

---

So if you're looking to decompress after a long week and relax, check out the LAX conversion functions for handling JSON conversions in BigQuery.

There are 4 separate functions: `LAX_STRING`, `LAX_BOOL`, `LAX_FLOAT64`, `LAX_INT64` - with each one of them attempting to convert a JSON value into the respective datatype.

This is a bit like using SAFE\_CAST - you won't get an error if the casting fails, just a NULL (so watch out, check the comments for an example when this can come to back to bite you).

Just note that even JSON-like string won't work as an input, it only works for the native JSON type.

As usual, watch out because these conversion functions might work differently as how you'd expect. SAFE\_CAST('1' AS BOOL) =&gt; NULL but SAFE\_CAST(1 AS BOOL) =&gt; TRUE.

![](https://miro.medium.com/v2/resize:fit:700/0*Kqn0tqN5Q74Pfazw align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://notjustsql.com)*.*