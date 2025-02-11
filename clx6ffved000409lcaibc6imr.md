---
title: "A couple of fun things about NULL in SQL"
datePublished: Sat Jun 08 2024 18:06:34 GMT+0000 (Coordinated Universal Time)
cuid: clx6ffved000409lcaibc6imr
slug: a-couple-of-fun-things-about-null-in-sql
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/5B0IXL2wAQ0/upload/8e1160c407fda3b5b40f000a2369760c.jpeg
tags: analytics, google-cloud, sql, bigquery, data-engineering

---

If you ever worked with SQL, even a tiny bit, you know NULL is very special value. Like no other. It's very different than an empty string '' or 0, rather representing the absence of a value.

A couple fun things about it:  
🔹 you cannot test if NULL is in a list of values: NULL IN (NULL) returns a NULL  
🔹 both (NULL = NULL) and (NULL &lt;&gt; / != NULL) are not allowed  
🔹 COUNT(column) counts non-null occurrences in a column, whereas  
COUNT(\*) or COUNT(1) counts all rows, including those with NULLS  
🔹 main aggregate functions ignore such SUM, COUNT, MIN, MAX, AVG ignore rows with NULLS; NULL is not the smallest value, it's just NULL, but  
🔹 ORDER by shows NULLS first by default when sorting ascending  
🔹 since a NULL not equal (not even comparable) to another NULL, upon joining, NULL values are not going to be matched

You can handle NULLS with:  
🔹 x IS NULL/ IS NOT NULL : checks if something is or is not a NULL  
🔹 COALESCE: take first non-null value in a list of values  
🔹 IFNULL/ISNULL: if null, use a backup value  
🔹 NULLIF: replace this value with a NULL

![](https://miro.medium.com/v2/resize:fit:1296/0*2OJE2DjSL3XkI7KH align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://notjustsql.com)*.*