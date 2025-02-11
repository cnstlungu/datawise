---
title: "A simple data validation scenario using FULL OUTER JOIN & ORDER BY"
datePublished: Thu May 02 2024 21:42:55 GMT+0000 (Coordinated Universal Time)
cuid: clvprvklh000208k30ckvhkxs
slug: a-simple-data-validation-scenario-using-full-outer-join-order-by
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/9k36QqhA0cU/upload/a6460c47662f78ede53388f470648933.jpeg
tags: analytics, google-cloud, sql, bigquery, data-engineering

---

Data Engineers do a lot of Data Analysis work, too.

For example: we need to understand why is there a difference between two approaches or data in two source systems.

[I've previously shown how a FULL OUTER JOIN](https://datawise.dev/comparing-tables-with-full-outer-join) in SQL with simple validation and how you [can ORDER BY an expression](https://datawise.dev/order-by-expressions-in-sql).

Let's look at a scenario where we can combine the two.

So we've got two source systems A and B, which *in theory* should provide the same sales figures, but they don't.

Understanding the difference between the two sources means identifying individual cases where the values are different, starting with the biggest discrepancies.

In the example below, we're going to order the results by the absolute value (ABS) of the difference between the figures in two systems, considering a missing value as 0.

This way, we can start our investigation from the biggest differences, regardless of which system shows 'bigger' values and also take into account missing values between the two.

![](https://miro.medium.com/v2/resize:fit:1400/0*n_ruvjFtLYWmzSwj align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](http://notjustsql.com)*.*