---
title: "Calculating the Median in BigQuery"
datePublished: Fri Aug 09 2024 15:00:51 GMT+0000 (Coordinated Universal Time)
cuid: clzmu3u3100030ams8f76fylo
slug: calculating-the-median-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/ARh8UV5dNxg/upload/bb6ee5ecf20047774843ebc3c83fb19b.jpeg
tags: analytics, statistics, google-cloud, sql, bigquery

---

One of these days, I had to handle missing value imputation and stumbled upon the need to calculate a median in BigQuery SQL. Since there is no built-in function for this, I looked for what other people used as workarounds—see sources in comments.

First, we have `PERCENTILE_CONT` and `PERCENTILE_DISC` (from continuous and discrete, respectively). The difference between them lies in whether interpolation is used:  
\- `PERCENTILE_CONT` uses linear interpolation. In the case of an even number of values, it returns their average.  
\- `PERCENTILE_DISC` selects the closest value without any interpolation.  
Both of these are window functions, so if you want to simulate grouping, you need to ensure that a single value is kept per group. Also, note the option of IGNORE | RESPECT NULLS (ignore is the default).

Additionally, we can use the approximate aggregation function `APPROX_QUANTILES`, which allows grouping. This function splits the values into quantiles, from which we can select the 50th percentile to retrieve the median. Check out the comments for a quick into intro approximate aggregate functions.

![](https://miro.medium.com/v2/resize:fit:1400/0*wWZC6J6Kiav7tW2Y align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://notjustsql.com)*.*