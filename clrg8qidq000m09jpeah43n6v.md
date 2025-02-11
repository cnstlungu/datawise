---
title: "DATETIME vs TIMESTAMP in BigQuery"
datePublished: Tue Jan 16 2024 10:58:21 GMT+0000 (Coordinated Universal Time)
cuid: clrg8qidq000m09jpeah43n6v
slug: datetime-vs-timestamp-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/rBPOfVqROzY/upload/d54409a8ff06a9ce2329da99aaedddcb.jpeg
tags: analytics, google-cloud, sql, bigquery, data-engineering

---

DATETIME and TIMESTAMP in BigQuery are not the same and should not be used interchangeably!

One thing I encounter from time to time is mixing of DATETIME and TIMESTAMP types. Even casually converting TIMESTAMP(DATETIME\_COLUMN) with no timezone provided.

This should not be done and you will get a type mismatch error when you, for example, try to compare them, for a very good reason.

What's the difference?

➡ DATETIME is a local time, happening once per day across the globe, at different points in time - it's 17:00 on January 12 first in Tokyo, then Bangalore, London and finally Los Angeles.

➡ TIMESTAMP is an absolute point in time and uses the UTC as a reference.

You can of course convert between the two, but you will NEED to provide a timezone context:  
\- if starting with a DATETIME, you need to provide a source timezone for the TIMESTAMP to be computed  
\- if you have a TIMESTAMP, you need to provide a target timezone for the DATETIME to be computed.

See below an illustration of how it's done.

![](https://miro.medium.com/v2/resize:fit:1400/0*uEL5ctXUw98kEf0- align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*