---
title: "Sometimes, you have to use subqueries!"
seoTitle: "Embrace the Power of Subqueries!"
seoDescription: "Learn how to handle SQL subqueries to filter errors and construct arrays, even with NULL values in your database"
datePublished: Fri Nov 01 2024 15:40:11 GMT+0000 (Coordinated Universal Time)
cuid: cm2ywhzrd000a09kxhhzxayso
slug: sometimes-you-have-to-use-subqueries
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/PkrUN6pvLYM/upload/8bc66d4d0cde961df587fbcf10cff73b.jpeg
tags: databases, google-cloud, sql, bigquery, data-engineering

---

Query without FROM clause cannot have a WHERE clause, goes the old SQL adage.

So I had this interesting problem the other day. Let's say an order has three boolean flags, each indicating whether a particular error has occurred during its lifetime. Our task is to create an array of all the errors that occurred for each order.

In order to solve it, we:  
\- create a scalar subquery  
\- since the flags can have the NULL value, we'd need to filter them out before passing them to the arrays constructor (which doesn't like nulls)  
\- create the array using the ARRAY () constructor

![](https://miro.medium.com/v2/resize:fit:1400/0*H5wMXGo3lbMiMyF3 align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [https://www.notjustsql.com](https://www.notjustsql.com/)*.*