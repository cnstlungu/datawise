---
title: "JSON datatype vs JSON-like STRING in BigQuery"
datePublished: Tue May 07 2024 13:19:46 GMT+0000 (Coordinated Universal Time)
cuid: clvwf3rsr000b09jthofy0499
slug: json-datatype-vs-json-like-string-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/0W4XLGITrHg/upload/f0b752b82d9f036b8d853963793ac1f6.jpeg
tags: analytics, google-cloud, sql, bigquery, data-engineering

---

In [one my previous posts](https://datawise.dev/the-json-datatype-in-bigquery), we've briefly introduced the JSON datatype in BigQuery.

But did anyone notice how most of the JSON functions have signatures for both a JSON-type input and a json-formatted string input?

What is the difference between the two?

Well, I like to call the json-formatted STRING a "json-like string" because while it might look like it, it's not necessarily valid JSON.

When you use, say, JSON\_VALUE to query such a string, it does not validate it and reads it from the start until (and if) it finds the key matching your query. It does not care that you gave it invalid JSON.

In the example below, the json-formatted/json-like string is missing a closing bracket "}", but JSON\_VALUE using it still manages to retrieve the 'key' since it never reaches the missing bracket .

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1715087932426/155be5b0-29cf-4d10-ba65-869c3e3b2d97.jpeg align="center")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](http://notjustsql.com)*.*