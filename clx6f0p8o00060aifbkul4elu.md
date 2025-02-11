---
title: "FLOAT vs NUMERIC in BigQuery"
datePublished: Sat Jun 08 2024 17:54:47 GMT+0000 (Coordinated Universal Time)
cuid: clx6f0p8o00060aifbkul4elu
slug: float-vs-numeric-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/yD5rv8_WzxA/upload/5604bbe3bb297e135649d0bcfd71b1a4.jpeg
tags: analytics, databases, google-cloud, sql, bigquery

---

What are the differences between FLOAT (FLOAT64) vs NUMERIC data types in BigQuery SQL and when to use each?

While they both can express decimals, they have some important differences in terms of precision and performance.

🔷 FLOAT (FLOAT64): a double-precision floating-point number.

Pros:  
\- can express a large array of values, both large and very very small.  
\- uses 8 logical bytes (half as compared to NUMERIC)  
\- calculations can be faster  
\- we have literals for not-a-number `NaN`, minus/plus infinity

Cons:  
\- it's an approximate data type, yielding potential rounding errors

Use cases  
\- queries that can tolerate small differences i.e. how many kg of chocolate we eat per capita per year  
\- scientific calculations with very large numbers

🔷 NUMERIC: a fixed-point decimal type for up to 38 digits, 9 decimal places, alias for DECIMAL

Pros:  
\- exact storage avoiding rounding errors, no loss of precision

Cons:  
\- uses 16 logical bytes  
\- calculations can be slower

When to use it:  
\- anywhere every single decimal digit matters, like finance or sending a spaceship to another planet

P.S. There's also BIGNUMERIC (alias for BIGDECIMAL) if you need even larger range, but that takes 32 logical bytes.

![](https://miro.medium.com/v2/resize:fit:1164/0*Ou0PlgTnOyftqi0t align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://notjustsql.com)*.*