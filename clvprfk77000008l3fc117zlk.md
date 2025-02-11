---
title: "The JSON datatype in BigQuery"
datePublished: Thu May 02 2024 21:30:28 GMT+0000 (Coordinated Universal Time)
cuid: clvprfk77000008l3fc117zlk
slug: the-json-datatype-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/KgLtFCgfC28/upload/c169391b2491e7b4201eff4266305665.jpeg
tags: analytics, databases, google-cloud, sql, data-engineering

---

The JSON datatype in BigQuery. This topic has been sitting in my Notion list of post ideas for some time.

So in our beloved BQ it is a native, standalone data type, not just another STRING 😁, although strings can of course hold json-like strings.

As data engineers we typically consume them in our pipelines, but let's first understand how to create them.

There are a couple of ways to express a JSON value:  
\- using the JSON literal  
\- by parsing a json-like STRING with JSON\_PARSE()  
\- from SQL objects (including an entire row) with TO\_JSON()  
\- creating a json\_object from key-value pairs with JSON\_OBJECT()  
\- creating a JSON\_ARRAY() from BQ ARRAY

Note that, for some of the above options, since JSON also have quotes, use multi-line strings """ """ or escape quotes with \\.

Defining our JSON objects as such will allow us to use JSON functions with them and, of course, store heterogeneous data in the same column.

Stay tuned for the next posts on this topic.

![](https://miro.medium.com/v2/resize:fit:1400/0*JwWzKCzKIjp1_27S align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](http://notjustsql.com)*.*