---
title: "Using SELECT * with EXCEPT and REPLACE"
datePublished: Thu Nov 30 2023 12:27:11 GMT+0000 (Coordinated Universal Time)
cuid: clpl67psm000509jm1qh1gms1
slug: using-select-with-except-and-replace
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/G1yhU1Ej-9A/upload/2090cc46a564b319574845af663b4590.jpeg
tags: analytics, sql, bigquery, data-engineering

---

`SELECT *` is not a good practice in production, but I still use it for spot checks, when debugging, analyzing or validating data - especially when working with wide tables.

Here are two useful clauses to keep in mind when working with `SELECT *` in BigQuery: `EXCEPT` and `REPLACE`.

➡ `EXCEPT` will exclude one or more columns from the output.  
➡ `REPLACE` will swap the enumerated columns with the new definitions you provide.

Also, since `SELECT DISTINCT *` won't work when you have a `STRUCT` column, you can use `EXCEPT` to exclude struct columns.

Let's look at an example. Say we'd like to select all the columns but exclude the Salary and modify the CustomerId.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701347070492/45cce5f8-ae4c-42a7-93b0-dbffa9630ae1.png align="center")

Here's how the code would look:

```sql
SELECT * 

EXCEPT(Salary) 

REPLACE(CONCAT('SystemA','-',CustomerId) AS CustomerId) 

FROM `learning.Customers`
```

This would produce the following output!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701347096531/0340d778-2418-4f48-9e17-6245438448c5.png align="center")

Thanks for reading!

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*