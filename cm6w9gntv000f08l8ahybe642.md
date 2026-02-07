---
title: "Extended data type support for BigQuery search indexes"
seoTitle: "Expanded BigQuery Search Index Data Support"
seoDescription: "BigQuery's search index for INT64 and TIMESTAMP improves performance with large datasets, enhancing real-world applications"
datePublished: Wed Nov 13 2024 22:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cm6w9gntv000f08l8ahybe642
slug: extended-data-type-support-for-bigquery-search-indexes
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/afW1hht0NSs/upload/4195cb00ad1acf4a11c41976a30c7326.jpeg
tags: analytics, databases, sql, bigquery, data-engineering

---

So, a couple of months ago, I posted about [BigQuery search indexes](https://datawise.dev/search-indexes-in-bigquery), interesting to those who work with large volumes of STRING or JSON data.

Recently, I came across a blog post introducing, in preview, the indexing of INT64 and TIMESTAMP columns as well.

Now, this brings interesting applications when working with big and huge tables, logs, or JSON data. You can partition only by one field and cluster by another four. You can’t partition or cluster by fields belonging to a STRUCT. Now this , using a SEARCH INDEX with integers and timestamps allows for a more efficient retrieval in such scenarios.

The referenced blog post (in comments) presents some pretty impressive improvements over not using search indexes.

I’ve played a bit with it but still haven’t managed to get the index to be used (which, last time, with STRING columns, I did). Perhaps something is wrong with the sample data (although not the size; I tried with a ~200 GB table), need to dig some more.

Does anyone use this feature in the real world?

![](https://miro.medium.com/v2/resize:fit:700/0*XCoHc26zCQqGQBxI align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [https://www.notjustsql.com](https://www.notjustsql.com/)*.*