---
title: "RANGE data type in BigQuery"
datePublished: Thu Mar 21 2024 14:52:10 GMT+0000 (Coordinated Universal Time)
cuid: clu1cpkby00030ajn1zk6dj9q
slug: range-data-type-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/MPOwVcXSVAI/upload/6f672cf1aa2903bc5a1f9c6650427957.jpeg
tags: analytics, sql, google-cloud-platform, bigquery, data-engineering

---

I work quite a lot with temporal/SCD2 type table so the new (still in preview) RANGE data type in BigQuery (and its supporting methods) are a welcome addition.

What does it do?

So instead of storing valid\_from & valid\_to in separate columns, we now have a datatype to store the time segment in an \[valid\_from, valid\_to) interval, of the form:

`SELECT RANGE(DATE '2021-01-01', DATE '2023-01-01').`

Note that the interval is left closed, right open (so left bound is included while the right one not).

This new semantic comes with a set of compatible functions :

\- constructors for RANGE and arrays of RANGEs

\- RANGE\_START and RANGE\_END to determine start and end of a segment

\- RANGE\_OVERLAPS, RANGE\_INTERSECT and RANGE\_CONTAINS to test the existence of an overlap, obtain the segment that overlaps and test the inclusion of a RANGE in another RANGE , respectively

While perhaps not a game changer, I still find the value in this upcoming feature.

Again, since this is still in preview it is not yet ready to use used in production.

See below an illustration of how it is used.

![](https://miro.medium.com/v2/resize:fit:1400/0*8ttj5oWnajbsrPVI align="left")

*Found it useful? Check out to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*