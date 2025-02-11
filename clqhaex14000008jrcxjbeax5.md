---
title: "Optimizing storage costs in BigQuery"
datePublished: Fri Dec 22 2023 23:53:23 GMT+0000 (Coordinated Universal Time)
cuid: clqhaex14000008jrcxjbeax5
slug: optimizing-storage-costs-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/NeTPASr-bmQ/upload/60505511ac0d4278a94c41f75c1a6939.jpeg
tags: google-cloud, bigquery, gcp, finops

---

As promised on a previous post about [optimizing costs for compute](https://datawise.dev/optimizing-compute-cost-in-bigquery), I've promised a post about storage as well, so let's dive in.

So how does BigQuery charge for storage?

Two billing models - set at dataset level: logical and physical.

Logical table size is the default option, representing uncompressed size. It is cheaper per Gib (roughly half of physical) and you get time travel storage for free.

Physical storage represents compressed, actual size of physical bytes stored on disk. It's twice as expensive as logical and you need to pay for the time travel storage as well BUT if you have data that compresses well (for example by using arrays), you might be able to save storage costs.

Now, we can further split these down into:  
\- active storage: any table or partition (for partitioned tables) modified in the last 90 days  
\- long-term storage: a table or partition (for partitioned tables) that hasn't changed in the last 90 days, and is 50% cheaper than the active storage.

Here's what you can do to help bring these costs down:

\- Identify what is taking up storage space: Look at information schema views such as INFORMATION\_SCHEMA.TABLE\_STORAGE to find out what is taking up the space that you pay for.

\- Cleanup: Clean up unneeded data or archive in cheap long-term storage. Think about storing aggregated version of historical data and save on storage.

\- Leverage table clones and snapshots in BigQuery to save on storing redundant data

\- Shorten time travel window (which is 7 days by default) - if you would not need to restore this data or not for the entire 7 days, you can reduce this (dataset level) and store less data. A staging table that is recreated every time, for example, might not need the 7 days. Read more in the [post about BigQuery time travel](https://datawise.dev/using-bigquery-time-travel).

\- Leverage long-term vs short-term data: any table or partition that you don't modify for 90 days becomes 50% cheaper to store, so maybe don't rebuild massive historical tables every time you run the process.

\- Use the table and partition expiration settings: you can set particular tables or partitions to expire after a given time, so you don't store data that you don't need

Hope these tips are useful!

![](https://miro.medium.com/v2/resize:fit:590/0*Utzk5O5rhycnAhVd align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*