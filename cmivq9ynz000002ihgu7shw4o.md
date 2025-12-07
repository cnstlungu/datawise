---
title: "Flattening JSON arrays in BigQuery"
datePublished: Sun Dec 07 2025 12:57:58 GMT+0000 (Coordinated Universal Time)
cuid: cmivq9ynz000002ihgu7shw4o
slug: flattening-json-arrays-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/19tQv51x4-A/upload/cb5db8fd2460224984ae2de7ca2f1bf8.jpeg
tags: analytics, sql, google-cloud-platform, bigquery

---

I've noticed that a new JSON function has been added (in Preview) in BigQuery SQL - JSON\_FLATTEN().

It allows us to flatten JSON arrays and return a single flat ARRAY, no matter how many nested levels there are.

So where is this actually useful?  
➡️ Handling heterogeneous JSON where the nesting depth isn’t consistent  
➡️ Cleaning up malformed or jagged arrays  
➡️ Normalizing data before UNNEST so you don’t get arrays of arrays

Where I would not use it?

👉 Don’t use it when the hierarchy matters. Flattening removes structural context, so you lose information about where an element came from.

![No alternative text description for this image](https://media.licdn.com/dms/image/v2/D4D22AQHaKMBOnN69pA/feedshare-shrink_1280/B4DZr4kANvHwAc-/0/1765106779219?e=1766620800&v=beta&t=xbMgNk-lxwyroUHu-8B7jk223iJJt9iP6NhiiKdJbrI align="left")

*Found it useful? Check out to my Analytics newsletter at* [*notjustsql.com*](https://notjustsql.com)*.*