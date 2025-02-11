---
title: "Time Series functions in BigQuery"
datePublished: Tue May 07 2024 13:24:51 GMT+0000 (Coordinated Universal Time)
cuid: clvwfabc900070al205wdf0n2
slug: time-series-functions-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/LPRrEJU2GbQ/upload/ee8b797625f583e51b1c81bb571ec5ad.jpeg
tags: google-cloud, sql, bigquery, data-engineering, data-analytics

---

I've [posted some time ago](https://datawise.dev/rounding-timestamps-in-bigquery) about "rounding" timestamps and datetime values, but in the past few months BigQuery has added Time Series functions (in preview for now), making for a cleaner and simpler approach of this problem.  
  
We now have `DATE_BUCKET`, `DATETIME_BUCKET` and `TIMESTAMP_BUCKET` which will help us bucket dates, datetimes and timestamps, respectively.  
  
In the example below, we're specifying the bucket size to be 15 minutes and the function groups each of our event\_timestamps into their respective bucket.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1715088228767/ecaba854-7a48-4c45-afea-ca5c6f2d4166.jpeg align="center")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](http://notjustsql.com)*.*