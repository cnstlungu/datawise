---
title: "Transforming cumulative sums into monthly values"
datePublished: Thu Mar 27 2025 07:34:24 GMT+0000 (Coordinated Universal Time)
cuid: cm8r1fn2f000q09jy9kl73vgy
slug: transforming-cumulative-sums-into-monthly-values
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/eDPAGdaJ-GQ/upload/017e3c48422f8e65dbed45f8e6bfe784.jpeg
tags: analytics, databases, sql, bigquery, data-engineering

---

Here’s a quick BigQuery SQL exercise. I often work with cumulative aggregations, but it’s not every day that I need to reverse them—converting cumulative values back into monthly figures.

Let's look at an example.

The dataset provides cumulative sales per fiscal year (July 1st - June 30th in this case). Our goal is to determine the actual sales for each month.

How do we do it?

1. Identify the fiscal year each period belongs to. We can use a UDF (as shown) or retrieve this from a date dimension table.

2. Use the LAG window function to retrieve the previous cumulative value (partitioned by our grain + fiscal year and ordered by period).

3. Subtract the previous cumulative value from the current one to derive the actual monthly sales.

• For the first month of a fiscal year, there’s no previous value, so we default to 0 in case of a NULL there.

Things to watch out for:  
➡️ Gaps in the data: How do they impact the calculation? Are we okay with that?  
➡️ Grain considerations: Do we need to do this per department? Per country? If so, adjust the PARTITION BY accordingly.

![](https://miro.medium.com/v2/resize:fit:700/0*Wuw8he37UZSOsKiT align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [***notjustsql.com***](https://notjustsql.com/)*.*