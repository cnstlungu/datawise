---
title: "BigQuery Saves Your Query Results — Here's How to Find Them"
seoTitle: "Where BigQuery Saves Query Results: Temporary Tables Explained"
seoDescription: "BigQuery writes query results to temporary tables unless you choose a destination. Learn where to find them, how long they persist, and what changes when you save results explicitly."
datePublished: Thu Mar 05 2026 07:34:36 GMT+0000 (Coordinated Universal Time)
cuid: cmmd5h2n000sk2cnq4mai4mkc
slug: bigquery-saves-your-query-results-here-s-how-to-find-them
cover: https://cdn.hashnode.com/uploads/covers/641c1535429c76261884ecba/568372e9-ef3d-486c-af8c-3112a8601ec3.jpg

---

Ever run a heavy BigQuery SQL query, processed gigabytes of data — and then accidentally closed the tab or forgot to save the results? 😬

**Don't re-run it. Your results are still there.**

BigQuery automatically saves query results to an anonymous temporary table for **24 hours**. You can find it under **Job Information → Temporary Table**.

This is also the engine behind BigQuery's caching behavior: if you run the exact same query again within that window — with no changes — BigQuery serves results directly from cache, **at no charge**.

**One caveat worth knowing:** if your result set exceeds **10 GB** (that's the output, not the data scanned), it won't be cached. So for very large result sets, you'll want to write results to a permanent table explicitly.

![](https://cdn.hashnode.com/uploads/covers/641c1535429c76261884ecba/6951dc9e-636e-4687-bc09-c9a1fe5f59d4.png align="center")