---
title: "BigQuery Primary Key & Foreign Key constraints"
datePublished: Sat Sep 16 2023 13:46:35 GMT+0000 (Coordinated Universal Time)
cuid: clmm30xg7000408mj4dot9ber
slug: bigquery-primary-key-foreign-key-constraints
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/SzG0ncGBOeo/upload/fd65d0fc84aa7888f6a14f4777c1febf.jpeg
tags: analytics, databases, sql, bigquery

---

Recently, BigQuery introduced Primary Key and Foreign Key constraints. However, they differ from what we're accustomed to in traditional RDBMS. For instance, these constraints aren't currently enforced, and they can only be set between tables within the same dataset. This means you can insert a *customer\_id* that doesn't match any in the customer table, even with a foreign key in place.

Since this felt somewhat watered down, I initially thought they'd serve mainly for metadata purposes. For example, defining a key's reference to values from a certain dimension or establishing the granularity of a table.

However, after some research, I found a [blog post](https://cloud.google.com/blog/products/data-analytics/join-optimizations-with-bigquery-primary-and-foreign-keys) that shed light on how these constraints can enhance join optimizations in BigQuery. Contrary to my initial belief, they're not just for documentation.

I decided to test this. Using a data\_source table (~400k rows) partitioned by date and clustered by id, I needed to look up a unique identifier from another table.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699617570432/40d5d7ac-e2d5-4b2f-86e9-0858f395b165.jpeg align="center")

```python
ALTER TABLE testing.lookup_table ADD PRIMARY KEY (id) NOT ENFORCED;
ALTER TABLE testing.data_source ADD PRIMARY KEY (id, ds_date) NOT ENFORCED,
ADD FOREIGN KEY(id) references testing.lookup_table(id) NOT ENFORCED;
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699617584632/7ef3cddb-ad92-4c67-b441-f570e7096b01.jpeg align="center")

I compared query results from two tables without constraints (learning dataset) to their replicas with constraints (testing dataset), ensuring cached results were disabled.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699617604468/c48b7031-a151-452f-95db-4996a29b754c.jpeg align="center")

From my tests, the queries using tables with constraints showed a significant efficiency boost. While they're not a one-size-fits-all solution, it's evident that Primary and Foreign Key constraints can influence performance (as showcased in the aforementioned article).

I'm optimistic about these functionalities expanding and their restrictions easing in the future.

Thanks for reading!

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*