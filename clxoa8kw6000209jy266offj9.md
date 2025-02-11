---
title: "Replicating datasets across regions in BigQuery"
datePublished: Fri Jun 21 2024 06:00:47 GMT+0000 (Coordinated Universal Time)
cuid: clxoa8kw6000209jy266offj9
slug: replicating-datasets-across-regions-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/brOOz19UzQg/upload/c42baf17e7c9f6707680fcd792751b2b.jpeg
tags: analytics, databases, google-cloud, bigquery, data-engineer

---

So this has been up for almost a year, but I've just found out that [you can replicate datasets across regions in BigQuery](https://cloud.google.com/bigquery/docs/data-replication). Obligatory remark that this is still in preview.

This should help quite a bit if you're working with data distributed across multiple BQ regions.

A couple of years ago, when facing the same task, I had to resort to setting up recurring BigQuery Transfer Service jobs to move data across regions.

![](https://miro.medium.com/v2/resize:fit:1400/0*3B7pvXlDIMxyfPDv align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://notjustsql.com)*.*