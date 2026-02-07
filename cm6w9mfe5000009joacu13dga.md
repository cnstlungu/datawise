---
title: "Using EXISTS with LOGICAL_OR in BigQuery"
seoTitle: "BigQuery: Working with EXISTS and LOGICAL_OR"
seoDescription: "Learn to use EXISTS with LOGICAL_OR in BigQuery for efficient flag checks across orders in SQL"
datePublished: Sat Feb 08 2025 14:03:04 GMT+0000 (Coordinated Universal Time)
cuid: cm6w9mfe5000009joacu13dga
slug: using-exists-with-logicalor-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/SVpCSOCcCwA/upload/83787a615dc2b68fbc9761ae0782acf8.jpeg
tags: analytics, google-cloud, sql, bigquery, data-engineering

---

Long time, no see! Here's a quick SQL exercise that illustrates some important modern concepts.

So, we're given a list of updates per each order, and at each point in time we have some flags. Our goal here is to check for each order if there was any point in time when any of the flags had the value of 1.

![](https://miro.medium.com/v2/resize:fit:700/0*Aj_QXiXCyPVxOAEw align="left")

We solve this by:

➡️ UNNEST the ARRAY where the indicators are stored, doing so in an inline select. Yes, you can use WHERE to filter the output of FROM UNNEST().  
➡️ leverage EXISTS to only check the existence of such an entry (we don't want to retrieve it), resulting in a TRUE/FALSE result  
➡️ use LOGICAL\_OR aggregation function, grouped by order\_id, to check if there is at least one entry where the flag from the previous step was true for that grain.

Happy querying!

*Found it useful? Subscribe to my Analytics newsletter at* [https://www.notjustsql.com](https://www.notjustsql.com/) *.*