---
title: "A closer look at STRING_AGG in BigQuery"
datePublished: Sat Feb 08 2025 14:18:55 GMT+0000 (Coordinated Universal Time)
cuid: cm6wa6ta2000k08l83bbpaib4
slug: a-closer-look-at-stringagg-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/CNjfgzoY8JU/upload/d0f32c6eaa071f43897255ec6d6cbc3c.jpeg
tags: analytics, databases, google-cloud, sql, bigquery

---

Modern SQL engines have a wealth of aggregation functions.  
  
Here's a quick example that makes use ofBigQuery STRING\_AGG.  
  
What does it do?  
  
It aggregates all the values in a grouping, joined by a separator of our choice, creating a string of those joined values.  
  
We can of course choose to:  
  
➡️ keep only distinct values, as well as  
➡️ order the values in the newly created string  
  
so that, as in the below example, ("Card", "Cash") and ("Cash", "Card") both produce "Card~Cash", every time.  
  
Any interesting aggregation function that you use in your SQL dialect?

![No alt text provided for this image](https://media.licdn.com/dms/image/v2/D4D22AQEbaqkpGTbFug/feedshare-shrink_2048_1536/B4DZTR3GwrGkAw-/0/1738687672622?e=1741824000&v=beta&t=sfO9fw8q3lBn3x9kvEDvqty4hCfSGZnJfoMhG8bOX-o align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [***notjustsql.com***](http://notjustsql.com/)*.*