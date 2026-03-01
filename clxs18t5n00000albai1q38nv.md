---
title: "NON-EQUI joins in SQL"
seoTitle: "SQL Non-Equi Joins: Join on Range and Inequality Conditions"
seoDescription: "Non-equi joins use comparison or BETWEEN operators instead of equality to match rows across tables in SQL. A practical pattern for range-based lookups..."
datePublished: Sun Jun 23 2024 21:00:06 GMT+0000 (Coordinated Universal Time)
cuid: clxs18t5n00000albai1q38nv
slug: non-equi-joins-in-sql
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/3X8a5pxNG4k/upload/434785cdddf318f4e785f33ed3ed20e1.jpeg
tags: analytics, databases, google-cloud, sql, bigquery

---

So here's another post about SQL joins. Based on the type of condition we use for joining we distinguish equi joins and non-equi joins.

Simply put:  
\- equi joins: we're using the equality operator:  
tab\_a.column\_x = tab\_b.column\_y  
\- non-equi joins: other operators, like comparison, inequality or BETWEEN are used

While a good portion of the time we use equi joins to, say, lookup the department the employee is part of, non-equi joins are not uncommon either.

Moreover, sometimes we might use both equality and other operators for joining the same table.

Let's look at a simple non-equi join scenario below.

![](https://miro.medium.com/v2/resize:fit:700/0*N5ilMd6BBoLYbrWj align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://notjustsql.com)*.*

---

*Enjoyed this? Here are some related articles you might find useful:*

- [Self-joins in SQL](https://datawise.dev/self-joins-in-sql)
- [Anti-joins in SQL](https://datawise.dev/anti-joins-in-sql)
- [SEMI-JOINS in SQL](https://datawise.dev/semi-joins-in-sql)
- [NATURAL JOIN in SQL](https://datawise.dev/natural-join-in-sql)
