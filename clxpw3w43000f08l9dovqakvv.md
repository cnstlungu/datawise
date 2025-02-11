---
title: "Determining JSON types in BigQuery"
datePublished: Sat Jun 22 2024 09:00:46 GMT+0000 (Coordinated Universal Time)
cuid: clxpw3w43000f08l9dovqakvv
slug: determining-json-types-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/fvMeP4ml4bU/upload/5e1184f032874c1e2b65dcfb9b7be49e.jpeg
tags: json, databases, google-cloud, sql, bigquery

---

Here's a mildly interesting function if you're working with JSON in [BigQuery](https://www.linkedin.com/feed/hashtag/?keywords=bigquery&highlightedUpdateUrns=urn%3Ali%3Aactivity%3A7207023990232477698).

JSON\_TYPE takes in a JSON value and returns the name of the respective JSON type (object, array, string, number, boolean, null) as a STRING.

See below an illustration of it in action.

Also, given we use the native JSON datatype, notice how we can just access the first (\[0\]) element in an ARRAY or a field directly by dot notation.  
This you cannot do with a JSON-like STRING (not without parsing). Check out my [previous post about JSON vs JSON-like string](https://datawise.dev/json-datatype-vs-json-like-string-in-bigquery).

![](https://miro.medium.com/v2/resize:fit:1400/0*4R9wTsBI9y3VYCpr align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://notjustsql.com)*.*