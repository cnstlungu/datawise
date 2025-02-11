---
title: "Enumerating ARRAY elements in BigQuery using WITH OFFSET"
datePublished: Sun Mar 31 2024 08:00:26 GMT+0000 (Coordinated Universal Time)
cuid: cluf8ekzm000608l61vvhf85w
slug: enumerating-array-elements-in-bigquery-using-with-offset
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/RF5HrKt8pfk/upload/aa242dd53579b38ce5fa60e37f6155e7.jpeg
tags: analytics, databases, google-cloud, sql, bigquery, data-engineering

---

In a [previous post](https://datawise.dev/unnesting-arrays-in-bigquery) we've covered what ARRAYS are in BigQuery, their use cases and how to flatten them with UNNEST.

Quite important to mention, ARRAYS are ordered collections (like lists in Python) - you set up that order when creating it. By UNNESTING them, the order is no longer guaranteed.

In order to retrieve the order in which an element was in an array before UNNESTING (apart from ordering again by something in the array like a timestamp) you can use `WITH OFFSET`, which will yield an additional column, showing the 0-based index of the element in the original array.

![](https://miro.medium.com/v2/resize:fit:1400/0*C-hkWWzhOcpTLyZk align="left")

*Found it useful? Check out to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*