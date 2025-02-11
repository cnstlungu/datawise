---
title: "Using GAPS_FILL in BigQuery"
datePublished: Tue May 07 2024 13:29:13 GMT+0000 (Coordinated Universal Time)
cuid: clvwffxci000c09kz910d2sub
slug: using-gapsfill-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/MYKAZlzW6Nw/upload/d86e093d745a4e50f32e93beef26f9f5.jpeg
tags: google-cloud, sql, bigquery, data-engineering, data-analytics

---

Another new time series function in BigQuery in addition to the [ones previously presented](https://datawise.dev/time-series-functions-in-bigquery) is the `GAPS_FILL` table-valued function.

It allows us to fill in a time series (DATE, DATETIME, TIMESTAMP) with missing rows to a desired time grain.

Previously, one could have solved this by joining with a date dimension or by using GENERATE\_DATE\_ARRAY for example.

It's simpler now, you just need to provide:  
\- the table you'd like to fill in  
\- the column you'd like to fill in (for example a DATE column)  
\- the interval you'd like the filling in to happen (time grain of the table)

In the example below, it allows us to fill in the time series with 2 missing days.

Since it's a table-valued function, it acts like a table so you select FROM it.

Obligatory remark that this is in 'Preview' for now.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1715088678872/acb1f7a4-980a-4cf4-873e-5fc3b077e2e3.jpeg align="center")

*Found it useful? Subscribe to my Analytics newsletter at*[*notjustsql.com*](http://notjustsql.com)*.*