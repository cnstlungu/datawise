---
title: "Compacting date intervals in BigQuery"
seoTitle: "Optimize Date Intervals in BigQuery"
seoDescription: "Learn how to compact date intervals in BigQuery using a step-by-step SQL approach, perfect for merging adjacent data intervals seamlessly"
datePublished: Mon Jun 09 2025 20:38:02 GMT+0000 (Coordinated Universal Time)
cuid: cmbpk0f8q000202l89rg7hgly
slug: compacting-date-intervals-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/3cTpEK08lwg/upload/a0447ed619c674a9ef0250a0242bdc10.jpeg
tags: databases, google-cloud, sql, bigquery, gcp, data-engineering

---


Here's a practical BigQuery SQL exercise that highlights some important concepts as well is an interesting algorithm imho. I've pair programmed this with LLMs, if that's a thing 😎

Problem statement: compacting a SCD-2 table, essentially finding intervals that can be safely merged, turning two adjacent intervals with the same data into a single, bigger interval.

This particular input data guarantees these intervals cannot overlap (at the same grain), but there can be gaps. We're also talking about \[left-inclusive, right-exclusive) intervals.

![](https://miro.medium.com/v2/resize:fit:700/0*xL2thW2sDi8R1WPf align="left")

Here's a breakdown of how it all works:

1️⃣ we're starting by computing a hash of all the column of interest, excluding the grain (in my example: flag\_a, flag\_b)  
2️⃣ then we use LAG() over grain window to detect whether the current row starts right after the previous one and if the hashes (so the 'payload' of the two rows) match  
3️⃣ we mark the start of a new "segment" when either:  
\- attributes have changed (flags differ), so hash being different  
\- intervals are not adjacent (there are gaps)

4️⃣ use a cumulative SUM() over grain window to group rows into segment IDs

5️⃣ collapse each segment using MIN(valid\_from) and MAX(valid\_to)

We can now see that in our example that several intervals were merged into bigger ones.

*Found it useful? Subscribe to my Analytics newsletter at* [***notjustsql.com***](https://notjustsql.com/)*.*

---

*Enjoyed this? Here are some related articles you might find useful:*

- [Joining temporal tables in BigQuery](https://datawise.dev/practical-bigquery-joining-temporal-tables)
- [Generating a compact temporal table in BigQuery](https://datawise.dev/generating-a-compact-temporal-table-in-bigquery)
- [Aggregating Multiple SCD-2 Attribute Timelines in BigQuery](https://datawise.dev/aggregating-multiple-scd-2-attribute-timelines-in-bigquery)
- [Transforming cumulative sums into monthly values](https://datawise.dev/transforming-cumulative-sums-into-monthly-values)
