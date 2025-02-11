---
title: "Hands-on with DuckDB"
datePublished: Mon Sep 25 2023 20:58:27 GMT+0000 (Coordinated Universal Time)
cuid: clmzdezgc000809leg2dj34cp
slug: hands-on-with-duckdb
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/59yg_LpcvzQ/upload/51309fb68852dcc85703914914f1a3c8.jpeg
tags: analytics, sql, duckdb

---

The right tool for the right job, right?

When developing a basic application or testing a concept, an option could be SQLite. It's a self-contained database system that offers a SQL interface and conveniently stores data in a file on your device. Perfect for straightforward tasks.

But what if you need an OLAP solution? There's DuckDB. This in-process DBMS is great for extracting, processing, and analyzing data. It can even support an analytical application you're working on. It's also super-fast.

I've had the pleasure of using DuckDB to establish a Data Warehouse for a quick proof of concept \[link in comments\]. Pairing it with Apache Superset was interesting – a robust BI toolkit right there.

Many analytical workloads don't demand the vast scale of cloud data warehouses like BigQuery or Snowflake. DuckDB offers a simple yet very powerful alternative, making analytics more accessible to all.

How easy is it to use it? Simply download an executable and start querying your files.

![](https://miro.medium.com/v2/resize:fit:1400/0*Gydtij97UFV9YBq9 align="left")

Where can you use it? In the console, using a host of programming languages, and more recently in the cloud, with Motherduck, currently in beta, a new offering also based on DuckDB.

![](https://miro.medium.com/v2/resize:fit:1400/0*gXgK_X9K5AVh4tmz align="left")

![](https://miro.medium.com/v2/resize:fit:1400/0*juyTjv5d6EnktFO4 align="left")

Where do I see it applicable? Useful to DAs, DEs, and even those who only get started. One-off analysis, exploratory data analysis, super-fast DW for small-to-medium analytical apps, and prototypes. Anywhere else you might use a pop-up OLAP database. Further down, perhaps separate queues for workloads based on their size.

In the example below I'm using it to query a sample 9.3M row CSV file.

![](https://miro.medium.com/v2/resize:fit:1400/0*L9BzCsprOgeKputm align="left")

Since competition in the analytics space is a driving force for progress, I'm enthusiastic about what's to come next. Hopefully, further democratization of this space can happen, so that even smaller companies are empowered by analytics.

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*