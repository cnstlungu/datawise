---
title: "Why you should care about partition pruning in BigQuery"
datePublished: Thu Feb 22 2024 10:05:10 GMT+0000 (Coordinated Universal Time)
cuid: clsx24mzv000208l2anfg1qpb
slug: why-you-should-care-about-partition-pruning-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/_E0--SXVjZM/upload/4b25b9c6d3fd2e41a56ee7fa85c7d015.jpeg
tags: databases, sql, google-cloud-platform, bigquery, data-engineering

---

When it comes to performance improvements and cost savings, handling only as much data as we need is very important. And partitioning is a cornerstone here.

Now, when working with tables that are partitioned, BigQuery tries to exclude the partitions it does not need (akin to pruning a tree) based on filters (WHERE clause) and JOINS, thus saving you time and processing power (and money).

But it's not always that simple. If you perform operations on the partitioned field (say the date field in a date-partitioned table), Big Q might not be able to prune the table accordingly. So you'll end up processing the entire massive table, even though you were only after one single day.

There's an example below with this happening when converting the date to a different timezone, but I've seen it happen with other operations. Pruning would not work in MERGE statement sourced from two UNIONed partitioned tables.

Check the number of rows read from the table in the examples below.

![](https://miro.medium.com/v2/resize:fit:1400/0*oPeOh5LyT5w81Oqy align="left")

*Found it useful? Check out to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*