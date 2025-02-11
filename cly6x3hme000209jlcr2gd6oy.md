---
title: "Ingestion-time partitioning in BigQuery"
datePublished: Thu Jul 04 2024 07:00:32 GMT+0000 (Coordinated Universal Time)
cuid: cly6x3hme000209jlcr2gd6oy
slug: ingestion-time-partitioning-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/hFBsF-CX5eQ/upload/de0d0e31be8bfbabd57a1aa0e5b66c99.jpeg
tags: databases, google-cloud, sql, bigquery, dataengineering

---

Have you ever used ingestion-time partitioning in BigQuery?

It's a separate type of partitioning that distributes rows into partitions based on the time they land in BQ.

Once such a table is defined, you can query the pseudocolumns *PARTITIONDATE and* PARTITIONTIME.

As with other partition types, you can set up OPTIONS such as :  
\- partition\_expiration\_days = drops a partition after a given period of time  
\- require\_partition\_filter = forces a user to use a partition filter when querying

Reminder that if you're ingesting data via a BigQuery job (say using the bq CLI utility), you can also control which partition in this table you want to write to using a decorator e.g. `my_table$20240621`

![](https://miro.medium.com/v2/resize:fit:700/0*GtZ5fMeuMwfeKqCY align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://notjustsql.com)*.*