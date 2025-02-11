---
title: "MERGE ON FALSE in BigQuery"
datePublished: Sat Sep 16 2023 14:15:37 GMT+0000 (Coordinated Universal Time)
cuid: clmm429x400010amnfemogmp4
slug: merge-on-false-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/IGspc5Np3VM/upload/bceec909eaf0228127afa348908e9b19.jpeg
tags: analytics, databases, sql, bigquery

---

Merge statements are essential for crafting incremental datasets. They let us INSERT, UPDATE, and DELETE in a single command. 🛠️  
Recently, I dived into an [insightful blog post](https://levelup.gitconnected.com/powerful-feature-on-merge-statement-in-bigquery-i-e9c805b9bc9a) about the ON FALSE clause in merge statements. Ever heard of it?

Typical merge:

```sql
MERGE table1 AS target
USING table2 AS source ON table1.column = table2.column
WHEN MATCHED -- e.g., update target
WHEN NOT MATCHED BY source -- e.g., delete from target
WHEN NOT MATCHED BY target -- e.g., insert in target
```

But with ON FALSE in the merge\_condition? [BigQuery docs](https://cloud.google.com/bigquery/docs/reference/standard-sql/dml-syntax#merge_statement) call it a "constant false predicate", perfect for atomic DELETEs on the target and INSERTs from a source. Essentially, a REPLACE operation.

I tested this on some data, especially after my previous post on [Primary and Foreign Keys](https://hashnode.com/post/clmm30xg7000408mj4dot9ber). The outcomes are looking super promising.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699609332025/b42be118-1cc5-424b-9af7-bb9e8bb9a450.jpeg align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699609352708/4e3cd1b1-09e6-4dc8-af3a-3e31071dcfed.jpeg align="center")

Testing that the expected changes happened.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699609379703/e968583a-426b-466f-8378-ed1ea7ed012c.jpeg align="center")

Using the table version that has Primary Key and Foreign Key constraints has yielded even more impressive results.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699609396730/1fea2c8b-6e53-4c02-9010-06a5b989d17b.jpeg align="center")

Thanks for reading!

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*