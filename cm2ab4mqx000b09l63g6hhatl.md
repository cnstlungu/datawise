---
title: "Why partitioning tables is not a silver bullet for BigQuery performance"
datePublished: Tue Oct 15 2024 10:35:28 GMT+0000 (Coordinated Universal Time)
cuid: cm2ab4mqx000b09l63g6hhatl
slug: why-partitioning-tables-is-not-a-silver-bullet-for-bigquery-performance
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/7EhAf2dBthg/upload/1a842df01fbbd9b7237a06ac2130b284.jpeg
tags: analytics, databases, google-cloud, sql, bigquery

---

I recently encountered an interesting case that reminded me of a couple of things and taught me a few lessons.

When working with BigQuery tables, partitioning and clustering are often go-to operations. Typically, we would partition by a meaningful date (which helps with joins and watermarking in incremental loads) and cluster by columns that form part of the grain, common filters or are commonly used in joins (or within MERGE statements).

While working on a recent task, I had a hypothesis that didn’t quite pan out as expected. Here’s the scenario:

Let's say have two tables:  
\- orders\_per\_store, containing fields like order\_id, order\_date, and store\_id.  
\- order\_amounts\_unpartitioned, which holds order amounts but is unpartitioned and clustered only on order\_id. It doesn’t have any date field.

Since order\_id is a unique identifier, it's sufficient for joining. However, I hypothesized that transforming the order\_amounts\_unpartitioned table to a partitioned one using order\_date could improve performance. The idea was to leverage the same order\_date field for partitioning in both tables to optimize the join.

To test this, I ran an experiment in my sandbox project with ~5M orders. The results surprised me.

Results:  
\- The join with the original unpartitioned table (order\_amounts\_unpartitioned), clustered by order\_id, actually performed best in terms of cost and efficiency when joined on just order\_id.  
\- Contrary to my assumption, the option I thought would be more efficient—joining by both order\_date (the partitioning field) and order\_id—was significantly more costly.  
\- Lastly, joining with the partitioned table but using only order\_id — proved to be least efficient.

Key Takeaway: This served as a great reminder: clustering alone is often enough (and the best solution) to optimize query performance, especially when partitioning results in small partitions (the docs recommend at least 10 GB per partition!).

Partitioning by default isn’t always the best approach—particularly for smaller tables— so consider clustering carefully, including the order of clustered fields.

Ultimately, this reinforced the importance of validating assumptions through real-world testing.

The resource consumption varied significantly across runs (so avoid thinking in terms of precise percentages), but the relative performance rankings remained consistent. It should be also noted that these results might be different based on the querying patterns and needs.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1728988379261/ba64bdda-c357-4903-b2e3-17c71f5a673f.png align="center")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://notjustsql.com)*.*