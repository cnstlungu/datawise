---
title: "The first thing I do when analyzing a SQL table"
datePublished: Wed Jun 05 2024 21:12:04 GMT+0000 (Coordinated Universal Time)
cuid: clx2bqv0p000409l53q4he6fr
slug: the-first-thing-i-do-when-analyzing-a-sql-table
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/afW1hht0NSs/upload/5e1e9e2b86113622df91da988bd5266a.jpeg
tags: databases, sql, google-cloud-platform, bigquery, data-engineering

---

Here's one of the first things I do with SQL when I want to quickly assess the data quality in a table.

I would run a series of quick COUNTs, testing key attributes of the data, such as key columns being NULL, which can display the distribution of problematic data so it can be processed accordingly.

A good way to ensure data quality in a data pipeline is to have a good look at it in the first place.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1717621805610/46bca7d8-54be-4a46-8daf-96a870193625.jpeg align="center")

*Found it useful? Subscribe to my Analytics newsletter at*[*notjustsql.com*](http://notjustsql.com)*.*