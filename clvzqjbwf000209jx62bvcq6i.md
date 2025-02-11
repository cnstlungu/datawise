---
title: "The order in which you ROUND matters in SQL"
datePublished: Thu May 09 2024 21:03:06 GMT+0000 (Coordinated Universal Time)
cuid: clvzqjbwf000209jx62bvcq6i
slug: the-order-in-which-you-round-matters-in-sql
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/1Kqc8ymfMKY/upload/d03e3f7f20ed2d5df5ad88b83f899e07.jpeg
tags: databases, google-cloud, sql, bigquery

---

Rounding numbers in SQL is one of the simplest operation, but it's important to we pay attention to how we apply it.

1. Consider the sequence in which you apply rounding and aggregation functions.
    

When you ROUND a value and then aggregate it using functions like SUM or AVG, the outcome may differ significantly compared to first aggregating the values and then rounding the result.

![](https://miro.medium.com/v2/resize:fit:1384/0*soGTOf7P8C_xKQPp align="left")

As with all things, take into consideration your context and business problem you're trying to solve.

2. Be sure to use the proper rounding function for the job:  
    \- `ROUND` - nearest integer or decimal place (if specified) 1.4 =1 but 1.5 =&gt;2  
    \- `FLOOR` - largest integer that is not greater than our value 1.7 =&gt; 1  
    \- `CEIL`/`CEILING` - smallest integer than is not smaller than our value 1.4 =&gt; 2
    

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](http://notjustsql.com)*.*