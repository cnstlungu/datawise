---
title: "SEMI-JOINS in SQL"
datePublished: Wed Jun 19 2024 06:00:29 GMT+0000 (Coordinated Universal Time)
cuid: clxlfchot000209mj8iydd401
slug: semi-joins-in-sql
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/5E5N49RWtbA/upload/a12b5b107805282f5ac536e46f2547b1.jpeg
tags: databases, sql, bigquery

---

Continuing our series about lesser-know types of SQL joins, let's look at the SEMI-JOIN today.

What does it do?

Well, we filter the entries in the left table to only the keys found in the right table, but unlike an INNER JOIN, we:  
\- we only get the columns in the left table  
\- even if there's multiple matching rows in the right table, we're not duplicating rows in the left one.

How are we going to implement it? We're going to use WHERE + EXISTS + a correlated sub-query (notice the WHERE clause in the subquery).

In the example below, we're using a semi-join to see which of the products have been previously ordered.

![](https://miro.medium.com/v2/resize:fit:1274/0*16G5qHgu74BojSMT align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://notjustsql.com)*.*