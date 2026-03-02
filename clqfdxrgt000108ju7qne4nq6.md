---
title: "Optimizing compute cost in BigQuery"
seoTitle: "BigQuery Compute Cost: On-Demand vs Capacity-Based Billing"
seoDescription: "Explains the difference between on-demand and capacity-based BigQuery compute billing and how to optimize for each."
datePublished: Thu Dec 21 2023 15:56:29 GMT+0000 (Coordinated Universal Time)
cuid: clqfdxrgt000108ju7qne4nq6
slug: optimizing-compute-cost-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/SAYzxuS1O3M/upload/41944310c8da03951a83b0eb02c11eb1.jpeg
tags: google-cloud, bigquery, gcp

---


Let's talk money 💸 . Now that I've got your attention - more precisely, cost optimization as a regular user. As cloud data warehouse users, in addition to ticking off functional requirements and of course, getting the results in a timely manner, we care also about the costs.

BigQuery costs can be split into compute (what you process) and storage (what you store). Let's look at compute (I promise a post about storage, too).

So it's important to know that BigQuery has two billing models for compute: on-demand and capacity-based.

On-demand is pretty straightforward - you pay per amount of data scanned, say 7.5 $ per TB, depending on region. Imagine paying your 🍧 ice-cream by weight.

Capacity-based means your company has purchased a processing capacity, measured in slots, over a unit of time. Here you pay the reservation and not the amount of data you scan. Imagine paying your ice-cream per recipient that you fill. As long as it fits in, regardless of weight, you pay the fixed amount.

So how does optimizing for compute look like for a regular user? When trying out different approaches (especially for working with very big datasets):  
\- If your company is billed on-demand basis, aim for processing less data (see the top-right corner info BEFORE running the query). This means you will get billed less.  
\- If your company has capacity-based billing, aim for a lower slot time consumed (see execution details AFTER you've ran your query). This will ensure there is enough capacity for other workloads in your organization.

Now, they typically correlate, but there might be cases where you pick between a lower slot time or a lower amount of data processed.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703174024097/e78eca78-6f7a-4884-9f97-1a5a5968969b.png align="center")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*

---

*Enjoyed this? Here are some related articles you might find useful:*

- [Why partitioning tables is not a silver bullet for BigQuery performance](https://datawise.dev/why-partitioning-tables-is-not-a-silver-bullet-for-bigquery-performance)
- [Why you should care about partition pruning in BigQuery](https://datawise.dev/why-you-should-care-about-partition-pruning-in-bigquery)
- [Optimizing SQL queries in BigQuery](https://datawise.dev/optimizing-sql-queries-in-bigquery)
- [Optimizing storage costs in BigQuery](https://datawise.dev/optimizing-storage-costs-in-bigquery)
