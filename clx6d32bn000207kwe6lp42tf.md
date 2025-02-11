---
title: "The PARTITIONS view in INFORMATION_SCHEMA"
datePublished: Sat Jun 08 2024 17:00:38 GMT+0000 (Coordinated Universal Time)
cuid: clx6d32bn000207kwe6lp42tf
slug: the-partitions-view-in-informationschema
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/rhaS97NhnHg/upload/576d8945cc675bcd814ad30713c0c1ab.jpeg
tags: analytics, databases, google-cloud, sql, bigquery, data-engineering

---

Riding on the back of recent news that BigQuery table partition limit has just increased from 4k to 10k partitions, I wanted to talk a bit about the `PARTITIONS` view in `INFORMATION_SCHEMA`.

I've [previously posted about information schema views](https://datawise.dev/the-power-of-bigquery-informationschema-views), but this particular view allows us to get information about partitions in our partitioned tables.

Here's what we can find there:  
\- total rows in that partition  
\- logical & billable bytes for that partition  
\- storage tier (ACTIVE if modified in the last 90 days, LONG\_TERM otherwise which is 50% cheaper)  
\- last modified time

Now, let's focus this `last modified time` as it is quite useful when building incremental SQL pipelines. Looking at this field could tell you if data in one of your many partitions was changed since your last run and needs to be reprocessed.

Such a feature should help you in cases when you don't have a reliable watermark column to determine what changed since your last run.

![](https://miro.medium.com/v2/resize:fit:1400/0*Jct5PDrlJN6HNZsC align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://notjustsql.com)*.*