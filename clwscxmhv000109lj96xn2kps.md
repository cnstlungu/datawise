---
title: "Combining ANY_VALUE with HAVING in BigQuery"
datePublished: Wed May 29 2024 21:47:37 GMT+0000 (Coordinated Universal Time)
cuid: clwscxmhv000109lj96xn2kps
slug: combining-anyvalue-with-having-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/inI8GnmS190/upload/18347cec7520991144f016d2260294e2.jpeg
tags: databases, google-cloud, sql, bigquery, data-engineering

---

Here's another rather rare instance where I've used ANY\_VALUE in  
BigQuery. It's basically an aggregation function like SUM or COUNT except it retrieves a arbitrary value from the grouping.

I've posted [about ANY\_VALUE before](https://datawise.dev/using-anyvalue-in-bigquery), but today's query was a bit different.

In the example below, my goal is to find orders that contain a single value, belonging to a particular list of values.

In other words, which order consisted of exactly one item, with that being grapes or oranges?

We aggregate using COUNT to count the number of order lines in an order and ANY\_VALUE to pick a random value from the list of order lines.

We then filter the aggregate results using HAVING, keeping only order that have exactly one order line and that order line being a grape or orange.

With ANY\_VALUE of a single value being always that value, we can filter the result sets to what we need. It's entirely true that the same can be said of MIN or MAX for instance, but I think it would have been a little less obvious of why it was chosen like that.

As almost always with SQL, there are of course plenty of other ways to achieve the same result.

![](https://miro.medium.com/v2/resize:fit:1108/0*TNEI4D-xTILUJQva align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](http://notjustsql.com)*.*