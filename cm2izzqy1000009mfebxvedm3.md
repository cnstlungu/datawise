---
title: "Computing a hash aggregation in BigQuery"
datePublished: Mon Oct 21 2024 12:33:40 GMT+0000 (Coordinated Universal Time)
cuid: cm2izzqy1000009mfebxvedm3
slug: computing-a-hash-aggregation-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/nVqNmnAWz3A/upload/1e4f0873f25d177bb9e0eb02f14d7851.jpeg
tags: analytics, databases, google-cloud, sql, bigquery

---

So I've seen Snowflake has an HASH\_AGG function. When would we need it?

Every time we'd like to work out if ANY value in a group (or the entire table) has changed in any way, even a single extra blank space.

While BigQuery does not have it yet, we can still simulate it using the tools at hand.

Here's how we can do it:  
\- TO\_JSON\_STRING to create a STRUCT from each entire row (or create a STRUCT containing only the columns you care about)  
\- STRING\_AGG to aggregate all the json strings into a single value per group (or the entire table)  
\- FARM\_FINGERPRINT, a hashing function that will product the same output given only the exact same input, check my comment for more info

![](https://miro.medium.com/v2/resize:fit:1400/0*5h-UhctKNjHhnszC align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://notjustsql.com)*.*