---
title: "Intersect and Except in BigQuery"
datePublished: Mon Oct 30 2023 11:52:25 GMT+0000 (Coordinated Universal Time)
cuid: clocubl5o000e09lc0x9e5mbo
slug: intersect-and-except-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/HHtzGcZkRZY/upload/f56dc9fa833f0f8da3ce31ac2932c9a3.jpeg
tags: databases, sql, bigquery

---

Almost everyone working with SQL has used UNION and UNION ALL. But these are not the only set operations available in SQL. Meet INTERSECT and EXCEPT.

What do they do? As the name suggests they perform the following set operations:

* INTERSECT returns the common entries, all elements present both in A and B, so A ∩ B.
    
* EXCEPT returns the elements present in A, but not in B, so A **∖** B
    

I find them quite useful when doing data validation, although they can be easily replicated with JOINs.

It's worth noting that while BigQuery supports UNION ALL and UNION DISTINCT, we are required to specify DISTINCT for INTERSECT and EXCEPT. At the time of this writing, INTERSECT ALL and EXCEPT ALL are not supported.

Let's see an example of them in action. Say we have the following two inputs:

Input A:

![Rowset A](https://cdn.hashnode.com/res/hashnode/image/upload/v1698665039984/08e3f339-67b6-4e04-a54c-56ed886fed2d.png align="center")

Input B:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698665088070/5464f3d8-7804-4c24-9e2e-b38d635a6e34.png align="center")

Here's what the output of INTERSECT would look like:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698666405360/9ed88146-a993-47b8-8175-43354743092a.png align="center")

And EXCEPT:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698666658051/54d16d9f-fc34-4e5d-a01b-c7bc9b8c9482.png align="center")

Thanks for reading!

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*