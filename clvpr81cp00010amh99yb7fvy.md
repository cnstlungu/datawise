---
title: "SESSION_USER in BigQuery"
datePublished: Thu May 02 2024 21:24:37 GMT+0000 (Coordinated Universal Time)
cuid: clvpr81cp00010amh99yb7fvy
slug: sessionuser-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/yekGLpc3vro/upload/a75c076600c161f7c36012c8c30cbe48.jpeg
tags: databases, google-cloud, sql, bigquery, data-analytics

---

SESSION\_USER is currently listed as the only "Security" function in the BigQuery documentation. What does it do?

It can help you find out the email or the principal of the user that is running the query.

This might a person or a service account that is impersonated. As far as I know, one could only impersonate the service account when using the bq cli (and not the GUI).

I remember using SESSION\_USER / CURRENT USER in my SQL Server days as well.

The only use case I thought of was a poor man's row-level security for tables, effectively filtering the rows you can see based on who you are. But there is a proper solution for this problem - [Row-level access policies](https://datawise.dev/row-level-access-security-in-bigquery).

Any interesting use cases which involve SESSION\_USER in your projects?

![](https://miro.medium.com/v2/resize:fit:822/0*widCALaUA8Ek5e12 align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](http://notjustsql.com)*.*