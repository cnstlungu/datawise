---
title: "Aggregating Multiple SCD-2 Attribute Timelines in BigQuery"
seoTitle: "BigQuery: Aggregating SCD-2 Attribute Timelines"
seoDescription: "Learn how to aggregate SCD-2 attribute timelines in BigQuery using SQL techniques to preserve temporal context efficiently"
datePublished: Wed Jun 11 2025 19:22:01 GMT+0000 (Coordinated Universal Time)
cuid: cmbsc6dgv000202jrcn3p5zee
slug: aggregating-multiple-scd-2-attribute-timelines-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/bnZ8_95Q8NE/upload/885d24ef5d81125139dbf105bc1a6b95.jpeg
tags: analytics, databases, google-cloud, sql, bigquery, data-engineering

---

Here’s another practical BigQuery SQL exercise 💡

Say you have an input SCD2-style table with \[valid\_from, valid\_to) and key-value attributes. Now you want to determine which attributes were valid at the same time for a given grain (e.g. id).

To do this, we:

1️⃣ Build an anchor table of all change points (start and end dates), grouped by id.

2️⃣ Generate date ranges using LEAD() over the change points, so we know the next boundary.

3️⃣ Join back to the original table to find which rows were active within each \[valid\_from, valid\_to) segment.

4️⃣ Aggregate the key-value pairs as ARRAY&lt;STRUCT&lt;key, value&gt;&gt; to preserve temporal context.

We can now see that, for example, for the period between \[2023-01-05, 2023-01-08), for id = 2, B was true and A was false.

![](https://miro.medium.com/v2/resize:fit:700/0*al6Q7c7B2GwZ3sZC align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [***notjustsql.com***](https://notjustsql.com/)*.*