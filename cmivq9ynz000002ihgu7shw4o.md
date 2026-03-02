---
title: "Flattening JSON arrays in BigQuery"
seoTitle: "Simplify JSON Arrays in BigQuery"
seoDescription: "Learn how to use BigQuery's JSON_FLATTEN to handle complex JSON arrays efficiently without losing data context when hierarchy isn't important"
datePublished: Sun Dec 07 2025 12:57:58 GMT+0000 (Coordinated Universal Time)
cuid: cmivq9ynz000002ihgu7shw4o
slug: flattening-json-arrays-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/19tQv51x4-A/upload/cb5db8fd2460224984ae2de7ca2f1bf8.jpeg
tags: analytics, google-cloud, sql, bigquery

---


I've noticed that a new JSON function has been added (in Preview) in BigQuery SQL - JSON\_FLATTEN().

It allows us to flatten JSON arrays and return a single flat ARRAY, no matter how many nested levels there are.

So where is this actually useful?  
➡️ Handling heterogeneous JSON where the nesting depth isn’t consistent  
➡️ Cleaning up malformed or jagged arrays  
➡️ Normalizing data before UNNEST so you don’t get arrays of arrays

Where I would not use it?

👉 Don’t use it when the hierarchy matters. Flattening removes structural context, so you lose information about where an element came from.

![](https://miro.medium.com/v2/resize:fit:1236/0*1UoE8j3SpwNK3K-V align="left")

*Found it useful? Check out to my Analytics newsletter at* [*notjustsql.com*](https://notjustsql.com)*.*

---

*Enjoyed this? Here are some related articles you might find useful:*

- [The JSON datatype in BigQuery](https://datawise.dev/the-json-datatype-in-bigquery)
- [JSON datatype vs JSON-like STRING in BigQuery](https://datawise.dev/json-datatype-vs-json-like-string-in-bigquery)
- [Extracting keys from JSON in BigQuery](https://datawise.dev/extracting-keys-from-json-in-bigquery)
- [LAX JSON conversion functions in BigQuery](https://datawise.dev/lax-json-conversion-functions-in-bigquery)
