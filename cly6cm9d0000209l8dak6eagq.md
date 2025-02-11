---
title: "DECLARE and SET variables in BigQuery"
datePublished: Wed Jul 03 2024 21:27:16 GMT+0000 (Coordinated Universal Time)
cuid: cly6cm9d0000209l8dak6eagq
slug: declare-and-set-variables-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/FMAVXJXIdP8/upload/8406333bdcaf627e4fceba56b9da4718.jpeg
tags: databases, google-cloud, sql, bigquery, gcp

---

Here's a part of procedural language that I use quite a lot in BigQuery.

Whether you're looking to run a query based on a multiple values of a particular parameter, finding out the watermark for incremental loading or just doing some testing, you can DECLARE and SET variables you can reuse across your query.

A couple of ways to do it:  
\- we can declare a variable with no type, but we need to provide a default, from which the time will be inferred  
\- a variable can be declared together with the type and choose to assign a value at declaration or later with SET  
\- a sub query can also provide the implicit value and table of a variable

![](https://miro.medium.com/v2/resize:fit:700/0*bFW5nHNmqpI0Zqik align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://notjustsql.com)*.*