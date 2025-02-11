---
title: "Using FORMAT_DATE in BigQuery"
datePublished: Sun Apr 28 2024 21:29:54 GMT+0000 (Coordinated Universal Time)
cuid: clvk1nf6c000c08i671uk4kne
slug: using-formatdate-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/bwOAixLG0uc/upload/427cf85c9d93246d0c7fa3475a483c0c.jpeg
tags: databases, google-cloud, sql, bigquery, data-analytics

---

The code we write daily as Data Engineers is not necessarily complicated.

We're solving a lot of problems like the following:

Given a schedule per day of the week (Monday hours are 10:00 - 22:00 / 10 am - 10 pm), find out what was the schedule for a list of calendar days.

Here's how a BigQuery solution could look like:  
\- using FORMAT\_DATE we can extract the abbreviated week day (%a in the list of format elements for date and time parts, attached in comments)  
\- transform that match casing of the joined column  
\- (INNER) JOIN

How would your solution to such a problem look like?

![](https://miro.medium.com/v2/resize:fit:1400/0*hcqI67_VNRky8qKr align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*