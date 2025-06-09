---
title: "Cross-dataset foreign key relationships in BigQuery"
datePublished: Mon Jun 09 2025 21:12:58 GMT+0000 (Coordinated Universal Time)
cuid: cmbpl9ch9000102i870lugcnt
slug: cross-dataset-foreign-key-relationships-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/Rm3nWQiDTzg/upload/1af0e7259e348bd4243faad29e2dd788.jpeg
tags: analytics, databases, google-cloud, sql, bigquery

---

It turns out you can now (don't know since when though) create cross-dataset foreign key relationships in BigQuery hashtag#SQL. Previously this was only possible for tables that are in the same dataset (but there were workarounds).

While the performance gain when using these *unenforced* PK/FK constraints in general may be up for discussion, it's definitely nice to be able to see this table metadata there, including the table grain 👍

For a refresher on what these constraints are, see [my previous post](https://datawise.dev/bigquery-primary-key-foreign-key-constraints).

![graphical user interface, text, application, email](https://media.licdn.com/dms/image/v2/D4D22AQEGDMIhA0ZLaw/feedshare-shrink_2048_1536/B4DZc3mBWsGUAo-/0/1748984403859?e=1752105600&v=beta&t=ebAouJ4MrFc-B7MbqJl2SSQZKz4sobMSd7IJOhkxVSg align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [***notjustsql.com***](https://notjustsql.com/)*.*