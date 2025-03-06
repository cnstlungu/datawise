---
title: "Change history in BigQuery"
datePublished: Thu Mar 06 2025 15:44:40 GMT+0000 (Coordinated Universal Time)
cuid: cm7xip82g000009jz2esefw0n
slug: change-history-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/5IHz5WhosQE/upload/8e51a5949b7b388bd6a3ae6487e90811.jpeg
tags: databases, google-cloud, sql, bigquery, data-engineering

---

Ever needed to track what changed in a table and when? In data engineering, this is known as Change Data Capture (CDC)—a fundamental challenge when dealing with evolving datasets.

Now, the Change History features in BigQuery sound pretty interesting.

BigQuery SQL has had the APPENDS table-valued function (TVF) for some time now, which works well for append-only scenarios. But it didn’t capture updates or deletes.

A few months ago a CHANGES TVF was added, which provides visibility into UPDATE and DELETE operations.

Unlike APPENDS (which works right out of the box), you need to enable change history tracking manually either at table creation or with an `ALTER TABLE ... SET OPTIONS()` command.

To illustrate how it all works I've:  
1️⃣ Created a table 2️⃣ Inserted a row 3️⃣ Updated a row

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1741275797472/f1c699d1-6bc0-470c-afb3-e785d3fa9e46.jpeg align="center")

As you will be able to see:  
✅ APPENDS captures new rows only.  
✅ CHANGES logs updates too (as a DELETE + INSERT).

Key things to note:

⚠️ Both features are still in preview, so not production-ready.  
💰 Querying this data still incurs processing costs.  
⏳ CHANGES only tracks modifications older than 10 minutes.  
📦 Enabling Change History means extra storage costs for metadata.

Has anyone tried using these in real-life scenarios?

*Found it useful? Subscribe to my Analytics newsletter at* [***notjustsql.com***](https://notjustsql.com/)*.*