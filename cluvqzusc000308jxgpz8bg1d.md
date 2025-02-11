---
title: "Comparing tables with FULL OUTER JOIN"
datePublished: Thu Apr 11 2024 21:25:10 GMT+0000 (Coordinated Universal Time)
cuid: cluvqzusc000308jxgpz8bg1d
slug: comparing-tables-with-full-outer-join
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/8Zt0xOOK4nI/upload/02aea9c2fc3e540836a6d51435c04ff7.jpeg
tags: analytics, databases, google-cloud, sql, bigquery, data-engineering

---

Does your Data Engineering project use a data-diffing tool?

Say you're preparing to deploy a change to a prod table. You've changed the way some metrics are calculated and twisted some filters. How do you find out what's different between two tables? Identify expected vs unexpected differences?

If lacking a specialized tool for data-diffing (like Datafold, Recce ) perhaps the simplest validation you can do when comparing two tables (dev and prod versions for example) leverages the FULL OUTER JOIN (or FULL JOIN in some RDBMS).

Start with the grain. Is there any way you can bring the tables to the same grain?

Once you have aligned them to the same grain, you can now join on the respective keys and COUNT the occurrences you care about - what's missing from A, what's missing from B, totals overall. Depending on attributes, you can use other aggregate functions to assess differences - for example, does the SUM of sales amounts match in prod vs dev?

You could also leverage a hashing function + TO\_JSON\_ARRAY ([check my previous post](https://hashnode.com/post/clnylckm2000209mi5p3x3hvb)) to see which rows are different in the two tables.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712870631627/63ae4e6c-09e4-4f51-b7bc-080098fdb352.jpeg align="center")

*Found it useful? Check out to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*