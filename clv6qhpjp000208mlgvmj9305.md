---
title: "Understanding STRUCTS in BigQuery"
datePublished: Fri Apr 19 2024 13:56:31 GMT+0000 (Coordinated Universal Time)
cuid: clv6qhpjp000208mlgvmj9305
slug: understanding-structs-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/oHly4Tu-vQ4/upload/08c90aa58436d36e0f3ac228c5f2faec.jpeg
tags: analytics, databases, google-cloud, sql, bigquery, dataengineering

---

I've previously did a [short intro post about ARRAYS](https://datawise.dev/unnesting-arrays-in-bigquery) in BigQuery, but I do see from time to time people that are just getting started become confused about how are they different from STRUCTS and when should we use them.

Let's clarify this.

STRUCT = a bundle of "columns" inside a single column. STRUCTS fields have a mandatory data type (inferred or declared by you) and an optional name. You're still having one instance of each field, but this field can be an ARRAY of multiple things.

ARRAY = a bundle of "rows", a list inside a single row. They NEED to be of the same type - INT64, STRING, STRUCT etc. They cannot have another ARRAY directly under them, but you can get around that with an ARRAY(STRUCT(\[array\_inside\_struct\])

You can still combine the two as you want, nest them in multiple layers, as long as you don't have an ARRAY directly under another ARRAY.

Both of them you can compare but you cannot order by or group by.  
For STRUCT, you can totally ORDER BY or GROUP BY one of the fields in the STRUCT (as long as it's not a STRUCT or ARRAY itself).

When to use each? Let's look an example.

![](https://miro.medium.com/v2/resize:fit:1400/0*4pT8ICc5EsTIrytC align="left")

STRUCT = a bundle of fields that relate to the same "thing" - say your current address - city, street name, postal\_code etc. Helps with a cleaner, more intuitive schema. `TYPE = RECORD, MODE = NULLABLE`

ARRAY = a list of things (0, 1 or more) that are related to this observation, for example a list of instruments a person plays on. `TYPE = your_data_type, MODE = REPEATED`

ARRAY of STRUCTS = you have a list of "things" that you know multiple things about and want to keep the together i.e. certifications =&gt; (name, from\_date).  
Would also be good to store all them addresses a person ever had. `TYPE = RECORD, MODE = REPEATED`

*Found it useful? Check out to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*