---
title: "The relationship between ARRAY_AGG and UNNEST"
datePublished: Sat Jun 08 2024 18:26:00 GMT+0000 (Coordinated Universal Time)
cuid: clx6g4uh900000ajm1u87d5dg
slug: the-relationship-between-arrayagg-and-unnest
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/VhDgReMsz8w/upload/910ca1350e91fa8b0c28ce16e9acd9c9.jpeg
tags: databases, google-cloud, sql, bigquery, data-engineering

---

If you're working with nested data in BigQuery, you've might've seen UNNEST, which helps 'unpack' arrays into individual rows.

But there's also ARRAY\_AGG, which, if you haven't encountered it before, which takes all rows for your GROUP BY bucket and creates an ARRAY out of them.

So, in essence, ARRAY\_AGG and UNNEST are doing the exact opposite of each other.

Check my previous posts on the topic:

* [Unnesting ARRAYS in BigQuery](https://datawise.dev/unnesting-arrays-in-bigquery)
    
* [Using ARRAY\_AGG in BigQuery](https://datawise.dev/using-array-agg-in-bigquery)
    
    ![](https://miro.medium.com/v2/resize:fit:1400/0*KigrcBwQXKCQ6znq align="left")
    
    *Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://notjustsql.com)*.*