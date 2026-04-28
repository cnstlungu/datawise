---
title: "Accessing ARRAY elements in BigQuery"
seoTitle: "BigQuery Array Access: OFFSET, ORDINAL, SAFE_OFFSET, SAFE_ORDINAL"
seoDescription: "Access BigQuery arrays with OFFSET or ORDINAL, and use SAFE_OFFSET or SAFE_ORDINAL to return NULL instead of failing on out-of-bounds indexes."
datePublished: Sun Mar 31 2024 15:41:50 GMT+0000 (Coordinated Universal Time)
cuid: clufovy9d000108l2bzv3gn9t
slug: accessing-array-elements-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/q1x3cuziBsc/upload/e378680b9668652350058d71c7c48227.jpeg

---


So here's 3 ways we can access elements in a BigQuery array.

\- by index: array\[index\], starting at 0  
\- using OFFSET(index): array\[OFFSET(index)\], also starting at 0  
\- using ORDINAL(1-based index)), starting at 1

The above will return an "index out of range" error if they are out of bounds, so to get around that you can using SAFE\_OFFSET and SAFE\_ORDINAL.

If you'd like to see what position each elements resides at in the array, check [WITH OFFSET](https://hashnode.com/post/cluf8ekzm000608l61vvhf85w).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711899643049/e2566935-c617-4ba9-898d-e18472e7624a.png align="center")

*Found it useful? Check out to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*

---

*Enjoyed this? Here are some related articles you might find useful:*

- [Using ARRAY_AGG in BigQuery](https://datawise.dev/using-array-agg-in-bigquery)
- [UNNESTING ARRAYS in BigQuery](https://datawise.dev/unnesting-arrays-in-bigquery)
- [Leveraging ARRAYS in BigQuery for query performance](https://datawise.dev/leveraging-arrays-in-bigquery-for-query-performance)
- [Enumerating ARRAY elements in BigQuery using WITH OFFSET](https://datawise.dev/enumerating-array-elements-in-bigquery-using-with-offset)
