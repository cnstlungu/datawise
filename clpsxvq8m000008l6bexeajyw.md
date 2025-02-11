---
title: "SELECT AS STRUCT and SELECT AS VALUE"
datePublished: Tue Dec 05 2023 22:56:05 GMT+0000 (Coordinated Universal Time)
cuid: clpsxvq8m000008l6bexeajyw
slug: select-as-struct-and-select-as-value
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/oHly4Tu-vQ4/upload/61de6b9184e6bab7863259acadabd212.jpeg
tags: analytics, google-cloud, sql, bigquery, data-engineering

---

Ever heard about value tables in BigQuery? Well, neither have I, until I've seen them mentioned in the docs. So, while in a normal table, a row is made up of columns, in a value table the row is a STRUCT.

Say you UNNEST `order_lines` AS order\_line. The 'order\_line' here is a value table.

Now, with this out of the way, let's see how it is useful, we need to introduce `SELECT AS STRUCT` and `SELECT AS VALUE`.

➡ `SELECT AS STRUCT` - produces a value table but preserves the STRUCT type i.e. you're still going to have order\_line.product\_id or order\_line.unit\_price

➡ `SELECT AS VALUE` - produces a value table by unpacking the struct values

When can these be useful?

☑ You have a STRUCT with a lot of attributes and don't want to reference them manually  
☑ You want to create a separate table out of the values in a STRUCT, without unpacking each column  
☑ Use this as input for creating an array of STRUCTS  
☑ You're using ARRAY\_AGG to de-duplicate (see example in comments).

See below for an illustration of the differences between the two.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1701816911706/6e9c6c39-5180-4635-acf7-a01f8cd84984.png align="center")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*