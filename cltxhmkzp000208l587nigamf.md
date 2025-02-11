---
title: "DELETE + INSERT vs MERGE in BigQuery"
datePublished: Mon Mar 18 2024 21:58:44 GMT+0000 (Coordinated Universal Time)
cuid: cltxhmkzp000208l587nigamf
slug: delete-insert-vs-merge-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/HjBcAVWlxnE/upload/b39a3f530bcb117cac1d295d231243bf.jpeg
tags: analytics, databases, google-cloud, sql, bigquery

---

How do you merge changes from staging tables into target tables in BigQuery?

I've previously covered [swapping out partitions using bq command](https://datawise.dev/swapping-partitions-in-bigquery) and [using constant false predicate "MERGE on FALSE"](https://datawise.dev/merge-on-false-in-bigquery), but I've learned that you can [now DELETE entire partitions for free](https://cloud.google.com/bigquery/docs/release-notes#February_27_2024) (provided a filter on the partitioned column is used) from tables.

That means that instead of merging your changes the old-fashioned way, it might be well worth DELETING the days you would like to update and INSERTING the entire days data back sourced from the staging table.

Here's a comparison of the two approaches for the same source and destination tables. As you can see the amount of processed data can be wildly different between the two.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710780004269/a1911788-873b-4a7b-a93f-a8205d00aaf2.png align="center")

Happy querying!

*Found it useful? Check out to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*