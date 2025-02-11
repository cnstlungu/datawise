---
title: "The NOT NULL Constraint in BigQuery"
datePublished: Thu May 16 2024 09:43:45 GMT+0000 (Coordinated Universal Time)
cuid: clw92cmtw000m09mk8mj0ev4i
slug: the-not-null-constraint-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/5B0IXL2wAQ0/upload/5c0a2b3ff095170686b845efa59d6aec.jpeg
tags: analytics, databases, google-cloud, sql, bigquery, data-engineering

---

Are you using the NOT NULL constraint in BigQuery? This constraint is a staple when working with databases.  
  
So, when creating a table, you have the option to declare if a particular column is required and should not be null. We do that by simply adding the NOT NULL to the column declaration.  
  
You also can check it on an existing table by checking the column (field) MODE.  
  
It can have 3 values:  
\- NULLABLE (which is the default if you've haven't set anything)  
\- REQUIRED (if you've set NOT NULL for this columns)  
\- REPEATED (for ARRAYS).  
  
Upon trying insert or update data that will violated this constraint, the statement will fail.  
  
Overall, setting the right MODE for your field helps enforce your expectations about the data that should be inserted or updated in a particular table.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1715852546134/7a62192a-7cf9-437c-b37c-7ba97a6eaa6b.jpeg align="center")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](http://notjustsql.com)*.*