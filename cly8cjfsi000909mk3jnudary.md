---
title: "System variables in BigQuery"
datePublished: Fri Jul 05 2024 07:00:37 GMT+0000 (Coordinated Universal Time)
cuid: cly8cjfsi000909mk3jnudary
slug: system-variables-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/HAI-GVIEvSQ/upload/23ba8714f6514d4a0675386a455342ca.jpeg
tags: analytics, databases, google-cloud, sql, bigquery

---

Today's quick post is about system variables in BigQuery. What are they?

They are a special type of variables, available in scripts (multi-statement queries). You can use them to read (and sometimes write) query metadata during query execution.

Here's a couple of examples:  
\- `@@query_label` - read/write query labels, making easier for you to group your queries based on they are used for  
\- `@@time_zone` - read/write default time zone to use  
\- `@@script.job_id` - the job id of the current job

Check out below an example with slot\_ms (returns slot time in millis), bytes\_billed and creation\_date.

![](https://miro.medium.com/v2/resize:fit:700/0*IQjiIlhLlwCgBMJW align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://notjustsql.com)*.*