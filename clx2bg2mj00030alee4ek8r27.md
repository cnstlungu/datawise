---
title: "How LIMIT helps you save time in BigQuery"
datePublished: Wed Jun 05 2024 21:03:41 GMT+0000 (Coordinated Universal Time)
cuid: clx2bg2mj00030alee4ek8r27
slug: how-limit-helps-you-save-time-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/aBgxd8IZ0jo/upload/abf3552ea24fd794f22f44395519e66c.jpeg
tags: databases, google-cloud, sql, bigquery, data-engineering

---

Here's a basic thing that can save you a bit of time when analyzing data or validating data transformations.

So I've [previously posted](https://datawise.dev/table-sampling-in-bigquery) about how in BigQuery using LIMIT for query output does not yield any cost saving as it has no effect on amount on data being processed - just how many results are returned to you.

But there are still cases where I use LIMIT.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1717621339092/1a99eb8a-9601-44ba-a30f-54f54620e1ca.jpeg align="center")

Say I'm validating some data and I want to check an assumption I have about the data. For instance, knowing that even a few duplicate records exist indicates me that the problem exists and provides an example to investigate.

I do not need to know all the possible duplicates in the table, therefore I use LIMIT to get at least one observation that will contradict what I'm expecting.

And even with LIMIT, if I don't get anything back, it means that the query hasn't found any matching rows which validates my initial hypothesis.

On a big enough table, one could notice the query execution time difference between using LIMIT and not using it. Again, there is no cost difference, but your time also costs 😁.

P.S. This is not to say that LIMIT is completely irrelevant to performance in BigQuery. Check out [this post](https://datawise.dev/de-duplicating-with-rownumber-vs-arrayagg) for a case where LIMIT does make a difference!

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](http://notjustsql.com)*.*