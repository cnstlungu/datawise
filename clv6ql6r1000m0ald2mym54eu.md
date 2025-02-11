---
title: "Using STRUCTS for quick analysis in BigQuery"
datePublished: Fri Apr 19 2024 13:59:14 GMT+0000 (Coordinated Universal Time)
cuid: clv6ql6r1000m0ald2mym54eu
slug: using-structs-for-quick-analysis-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/-Vqn2WrfxTQ/upload/afc1d91e252f9be5a2461fe4311e2caf.jpeg
tags: google-cloud, sql, bigquery, data-engineering, data-analytics

---

I've posted earlier [about STRUCTS in BigQuery](https://hashnode.com/post/clv6qhpjp000208mlgvmj9305), here's how I use it from time to time to help me debug and analyze data a bit faster.

Since changing filter values for different test cases / observations you are interested about can be a headache (especially if you have a lot of columns), you could put them in a tuple of STRUCTS and check the matching records at once.

Not a game changer but makes life a bit easier 😁

![](https://miro.medium.com/v2/resize:fit:1400/0*jnxtlXlSrHzQqi6g align="left")

*Found it useful? Check out to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*