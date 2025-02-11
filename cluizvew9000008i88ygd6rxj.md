---
title: "Why you should use UNION DISTINCT sparingly"
datePublished: Tue Apr 02 2024 23:12:39 GMT+0000 (Coordinated Universal Time)
cuid: cluizvew9000008i88ygd6rxj
slug: why-you-should-use-union-distinct-sparingly
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/G1yhU1Ej-9A/upload/b946f2e1112d2bad3f74d236addedec2.jpeg
tags: analytics, databases, google-cloud, sql, bigquery

---

Let's help BigQuery do less unneeded work!

If you're UNIONING two sources known to have distinct values (and they don't have duplicates), go for UNION ALL instead of UNION DISTINCT (UNION for some other sql dialects) to avoid redundant de-duplication.

In the example below, I've unioned two Google Trends tables - one that is only for US terms and another one for the rest of the world. Since one table only contains US and the other everything except the US, we know the union of the two tables to be distinct from the start, thus not needing the UNION DISTINCT.

![](https://miro.medium.com/v2/resize:fit:1400/0*f_7wweJfDi_6rLDY align="left")

There's no difference indeed for on-demand pricing (same amount of data scanned), but quite a difference for capacity pricing users ( 1/2 of slot usage).

So use UNION DISTINCT (and any other DISTINCT) sparingly and when you actually need it.

*Found it useful? Check out to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*