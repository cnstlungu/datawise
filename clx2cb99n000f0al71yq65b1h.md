---
title: "Joining with USING vs ON in BigQuery"
datePublished: Wed Jun 05 2024 21:27:56 GMT+0000 (Coordinated Universal Time)
cuid: clx2cb99n000f0al71yq65b1h
slug: joining-with-using-vs-on-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/nShLC-WruxQ/upload/a18d8d63a4a119d9c8f0da010b93eb74.jpeg
tags: databases, google-cloud, sql, bigquery, data-engineering

---

What's the difference when joining with `ON` vs `USING` clause in BigQuery SQL flavor? I was quite surprised to see USING when moving from SQLServer.  
  
In short:  
➡ USING allows you to join tables where the columns you want to join on have the same names and you just test for equality: table1.column = table2.column. You enumerate these columns in the USING clause :  
  
`USING (columnA, columnB, etc)`  
  
➡ ON is the more general one, doing everything what USING does (but you need to spell out that equality), but also allowing you to join on inequalities, transforming on the fly in joining, filtering for a value, and pretty much any other way you'd need joining.  
  
`ON table1.columnA = table2.columnA` etc  
  
So yes, USING is pretty much syntactic sugar for a fairly common type of join, but still narrower in functionality than the good old ON.  
  
It's worth pointing out that with USING, the columns in the clause do not need an alias for disambiguation (making clear which one of the two tables we take the column from), effectively doing the same a COALESCE of the columns in the two tables would do.  
This helps you a little bit with FULL OUTER JOINS for example. Of course, for other columns, if there are clashes in the namespace, you do need to specify where do you want them sourced from.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1717622804042/b45f4f10-d8ad-4d49-92ea-fe7c557df51a.jpeg align="center")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*