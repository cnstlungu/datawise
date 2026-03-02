---
title: "Cross-dataset foreign key relationships in BigQuery"
seoTitle: "Link Foreign Keys Across Datasets in BigQuery"
seoDescription: "Learn to create cross-dataset foreign key relationships in BigQuery and explore metadata enhancements for SQL tables with ease"
datePublished: Mon Jun 09 2025 21:12:58 GMT+0000 (Coordinated Universal Time)
cuid: cmbpl9ch9000102i870lugcnt
slug: cross-dataset-foreign-key-relationships-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/Rm3nWQiDTzg/upload/1af0e7259e348bd4243faad29e2dd788.jpeg

---


It turns out you can now (don't know since when though) create cross-dataset foreign key relationships in BigQuery hashtag#SQL. Previously this was only possible for tables that are in the same dataset (but there were workarounds).

While the performance gain when using these *unenforced* PK/FK constraints in general may be up for discussion, it's definitely nice to be able to see this table metadata there, including the table grain 👍

For a refresher on what these constraints are, see [my previous post](https://datawise.dev/bigquery-primary-key-foreign-key-constraints).

![](https://miro.medium.com/v2/resize:fit:700/0*6jgUdm3tK8Kmdvam align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [***notjustsql.com***](https://notjustsql.com/)*.*

---

*Enjoyed this? Here are some related articles you might find useful:*

- [Row-level access security in BigQuery](https://datawise.dev/row-level-access-security-in-bigquery)
- [Using subqueries with Row Level Security in BigQuery](https://datawise.dev/using-subqueries-with-row-level-security-in-bigquery)
- [Why basic roles in BigQuery are a bad idea](https://datawise.dev/why-basic-roles-in-bigquery-are-a-bad-idea)
