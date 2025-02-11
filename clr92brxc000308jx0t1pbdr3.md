---
title: "Computing a cumulative sum in BigQuery"
datePublished: Thu Jan 11 2024 10:24:33 GMT+0000 (Coordinated Universal Time)
cuid: clr92brxc000308jx0t1pbdr3
slug: computing-a-cumulative-sum-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/_zsL306fDck/upload/07403402006ef0b113e240736b99fba9.jpeg
tags: analytics, google-cloud, sql, bigquery, data-engineering

---

How do you compute a cumulative SUM in BigQuery?

Today we're going to look at how to compute a cumulative sum in BigQuery, a scenario that pops up now and then and is quite easy to solve using window functions.

In the below example, we have a dataset representing customer orders. We'd like to find out the cumulative sum of each individual customer.

For this we'll need :  
\- SUM function combined with a WINDOW function call  
\- PARTITION BY customer ID to perform calculation at customer level  
\- ORDER BY order\_date (ascending by default) so that the values are summed up chronologically  
\- a window frame clause: ROWS BETWEEN UNBOUNDED (starting with the first entry) AND CURRENT ROW (until and including this row)

See below for an illustration of how it all works. Happy querying!

![](https://miro.medium.com/v2/resize:fit:1400/0*vQUYOA2yAJBu80uB align="left")

Bonus point: You can also use a [named window declaration](https://datawise.dev/tidying-up-window-functions-in-bigquery-with-named-windows) for cleaner code.

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*