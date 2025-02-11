---
title: "Generating date intervals in BigQuery"
datePublished: Tue Jan 16 2024 11:01:59 GMT+0000 (Coordinated Universal Time)
cuid: clrg8v677000b09jrd2doaq22
slug: generating-date-intervals-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/jqxB3C0YNG0/upload/66860e572b0360846c5f141452fd7d08.jpeg
tags: analytics, databases, google-cloud, sql, data-engineering

---

Ever had to generate a date interval in BigQuery?

Take a look at the GENERATE\_DATE\_ARRAY function.

Needs 3 arguments:  
\- start\_date  
\- end\_date  
\- interval step (DAY, WEEK, MONTH, QUARTER, YEAR)

Since it generates an ARRAY, we would need to UNNEST it to get one date per row.

If you need something more granular, there is the very similar GENERATE\_TIMESTAMP\_ARRAY, which can generate in increments between MICROSECOND and DAY.

Friendly reminder to not mix and match DATETIME and TIMESTAMP without properly converting between them beforehand - see [my previous post](https://datawise.dev/datetime-vs-timestamp-in-bigquery).

![](https://miro.medium.com/v2/resize:fit:1400/0*jf86uGe8Aurx-XvI align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*