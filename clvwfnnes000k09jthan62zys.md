---
title: "Where does QUALIFY fit in the order of execution in BigQuery?"
datePublished: Tue May 07 2024 13:35:13 GMT+0000 (Coordinated Universal Time)
cuid: clvwfnnes000k09jthan62zys
slug: where-does-qualify-fit-in-the-order-of-execution-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/qodjMu0byZ8/upload/a62ef63e338412e6b36c4769d5663fa8.jpeg
tags: analytics, google-cloud, sql, bigquery, data-engineering

---

Here's an example of how QUALIFY fits into the order of execution in SQL.  
  
In the BigQuery example below, we want to compute the second-to-last `order_updated` event for each order.  
  
To do this, we filter to keep only the rows WHERE order\_status = 'order\_updated'.  
  
We use there rows then to retrieve the event occurring second - sorting decreasingly by event\_ts and partitioning by order\_id, using QUALIFY.  
  
The output is then ORDER BY the second\_to\_last\_order\_update\_ts decreasingly.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1715088852613/6c027d44-2981-4952-a6a3-567abd42912e.jpeg align="center")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](http://notjustsql.com)*.*