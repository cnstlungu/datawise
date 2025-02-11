---
title: "Another look at LOGICAL_AND & LOGICAL_OR in BigQuery"
datePublished: Wed Jun 05 2024 21:21:22 GMT+0000 (Coordinated Universal Time)
cuid: clx2c2tb1000c0al75muh8nbw
slug: another-look-at-logicaland-logicalor-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/x649mR6yBIs/upload/051479c7af935b4e2a1223d21fcfe237.jpeg
tags: analytics, databases, google-cloud, sql, bigquery, data-engineering

---

Out of all those non-standard SQL functions in BigQuery, I think I like LOGICAL\_AND and LOGICAL\_OR the most.  
  
These are aggregation functions I've posted about before (link in my comments), but just wanted to showcase how versatile they can be.  
  
So:  
\- LOGICAL\_OR = at least one value in the grouping bucket is TRUE.  
\- LOGICAL\_AND = all the values in the grouping bucket are TRUE.  
  
Plenty of stuff you can do with it:  
\- pair them with NOT when needed  
\- since they're aggregation functions, you compute a result for a bucket with GROUP BY or you can opt for using a window function call OVER (PARTITION BY ...)  
\- if you opt for GROUP BY, you can opt for filtering output with HAVING; whereas if you go through the window function route, you have QUALIFY for that matter  
  
In the example below, I'm looking to compute three things about customers:  
\- are all their orders are paid?  
\- do they have any outstanding orders (i.e. not shipped yet)?  
\- whether they have ordered olives in the last 3 months  
  
I make use of LOGICAL\_AND and LOGICAL\_OR for that.  
  
As usual, one can achieve the same results using MIN and MAX, since:  
\- MIN(\[TRUE,..., FALSE\]) = FALSE AND MAX(\[TRUE,..., FALSE\]) = MAX.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1717622316132/569d4bbe-620d-4111-8c48-e36b90cc444f.jpeg align="center")

*Found it useful? Subscribe to my Analytics newsletter at* [*https://notjustsql.com*](https://www.notjustsql.com/)*.*