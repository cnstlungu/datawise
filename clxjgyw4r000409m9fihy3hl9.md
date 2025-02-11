---
title: "Anti-joins in SQL"
datePublished: Mon Jun 17 2024 21:10:22 GMT+0000 (Coordinated Universal Time)
cuid: clxjgyw4r000409m9fihy3hl9
slug: anti-joins-in-sql
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/eZas-0yTQqI/upload/8ce0e7ce76da45ecb1191f1b72d4ea29.jpeg
tags: databases, sql, bigquery

---

Here's the SQL Anti-Join, another type of join that doesn't have its own keyword but it's very much a thing. You might have used it a lot of times before 😁

So, what does it do?

The anti-join retains all the rows in one table that are not also found in another table. So A \\ B.

We achieve this with a LEFT JOIN + WHERE \[key in right table\] IS NULL for the LEFT ANTI JOIN and RIGHT JOIN + WHERE \[key in left table) IS NULL for the RIGHT ANTI JOIN (although I know right joins don't get much love here 😁).

An anti-join is a bit similar to the [EXCEPT set operation](https://www.linkedin.com/feed/update/urn:li:activity:7124727873818509312/), with the difference that:  
\- in the EXCEPT if at least one column is different between the two tables, the row is considered a difference (so is kept)  
\- in the ANTI JOIN we typically look at just whether the join keys are present in the other table or not (but you check as many columns as you want, of course)

In the example below, we're illustrating a LEFT ANTI JOIN which finds all the products we have details for (like product name) but for which we don't have a row in the pricing table.

![](https://miro.medium.com/v2/resize:fit:1308/0*FvwZTexztXSPfKTq align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://notjustsql.com)*.*