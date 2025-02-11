---
title: "Combining STRUCTs with Window Functions in BigQuery"
datePublished: Wed Oct 18 2023 17:30:12 GMT+0000 (Coordinated Universal Time)
cuid: clnw13rnp000409mj9fqs6nf0
slug: combining-structs-with-window-functions-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/P_qvsF7Yodw/upload/fe43c226c0e3d8a6be289a53a6efb097.jpeg
tags: analytics, data-analysis, google-cloud, sql, bigquery

---

How often do you use STRUCTs in BigQuery? I do a lot, and here's an interesting use case.

### **First, what is a STRUCT?**

So, if you're not familiar with them, a STRUCT is a data type used to represent an object, allowing us to group related fields within one data cell.

Think of it as the ability to store complex 'things' inside a BigQuery row, in addition to the 'primitive' types like INT64 or STRING. So you can have a STRUCT '*person'* that has attributes like name, age and salary. This can of course be REPEATED to obtain an ARRAY of person STRUCTs.

Now, STRUCTs are useful for many things, one of which I'm going to present today.

Here is a trick I use when working with window functions like LEAD and LAG that involve STRUCTs in BigQuery.

### Problem statement

Did you ever have to retrieve the historical attribute (previous or next) of an entity in a temporal table (SCD-type 2)?

Here's how an example could look.

```sql
SELECT 
    id, 
    value_int, 
    value_text, 
    valid_from, 
    valid_to,
    LEAD(value_int) OVER (PARTITION BY id ORDER BY valid_from) AS next_value_int,
    LEAD(value_text) OVER (PARTITION BY id ORDER BY valid_from) AS next_value_text,
    LAG(value_int) OVER (PARTITION BY id ORDER BY valid_from) AS prev_value_int,
    LAG(value_text) OVER (PARTITION BY id ORDER BY valid_from) AS prev_value_text
    
FROM `learning.input_data` 

ORDER BY id, valid_from
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697579982891/e1fcba3e-8956-41cd-905b-03aa53a981c7.png align="center")

Okay, but what if you have a dozen attributes? Instead of writing tens of LEAD or LAG functions, leverage STRUCT and look up an entire STRUCT of attributes.

### The solution

Here's an adapted example that uses STRUCTs.

```sql
WITH input_data AS (
    SELECT 
        id, 
        value_int, 
        value_text, 
        STRUCT(value_int, value_text) AS value, 
        valid_from, 
        valid_to
    FROM `learning.input_data` )
 SELECT 
     id, 
     value_int, 
     value_text, 
     valid_from, 
     valid_to,
     LAG(value) OVER (PARTITION BY id ORDER BY valid_from) AS prev_value,
     LEAD(value) OVER (PARTITION BY id ORDER BY valid_from) AS next_value
 FROM input_data

ORDER BY id, valid_from
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697581160565/63aa6e16-eb5a-4cf4-9451-3a346e60ec03.png align="center")

This way, you can use LEAD or LAG only once, regardless of how many attributes you need to look up.

There are of course other interesting use cases for STRUCTs, which we will explore in upcoming posts. Stay tuned!

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*