---
title: "Calculating the MODE in BigQuery"
datePublished: Wed Feb 21 2024 22:15:27 GMT+0000 (Coordinated Universal Time)
cuid: clswcrxmy000008l801rbgyb5
slug: calculating-the-mode-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/dBI_My696Rk/upload/c7fb8ba8e01bd4af10a95a75b3022cb0.jpeg
tags: analytics, statistics, google-cloud, sql, bigquery, data-engineering

---

How do you compute the MODE (most frequent value) in BigQuery?

For the other measures of central tendency like MEAN and MEDIAN, there are straightforward ways to compute results - functions AVG and PERCENTILE\_CONT/PERCENTILE\_DIST respectively, but there's no dedicated function for MODE.

By the way, if you have a huge dataset and can bear some lack of precision, take a look at APPROX\_TOP\_COUNT.

Say we have the following input data:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708553490924/574e8efa-e260-4dc0-b8b1-8e41d4a16dd8.png align="center")

Now here's how we can compute them otherwise:  
\- filter out NULLS (if we want to ignore them) or do nothing if we want to keep them  
\- compute value counts for our desired grain  
\- take the most frequent one per our grain using QUALIFY + RANK

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708553539348/88be7fdd-e864-4fa4-924f-cfec2d47b464.png align="center")

Here's how the output would look with NULLS excluded.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708553571790/e0ede638-19e6-4140-8a75-d49ebea22e92.png align="center")

And with them included:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708553662143/5cedea71-1150-4646-874a-eb941cec5ff7.png align="center")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*