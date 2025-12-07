---
title: "Table grain quick validation with SQL"
datePublished: Sat Oct 04 2025 12:22:56 GMT+0000 (Coordinated Universal Time)
cuid: cmgc8udua000f02kv63z0c0l9
slug: table-grain-quick-validation-with-sql
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/pcW5bR7gSJ4/upload/1348e2cccae0b01aab2ddf59f016dd1a.jpeg
tags: analytics, sql, google-cloud-platform, bigquery, data-engineering

---

I was doing some exploratory data analysis on a number of tables I didn’t have much information about and, unfortunately, didn’t know their grain.

I needed a quick way to validate my assumptions about the table grain, identify contradicting observations (rows), and check for duplicates at the same time.

Therefore I decided to use a combination of TO\_JSON\_STRING and FARM\_FINGERPRINT. The first creates a JSON representation of the entire row (given a table alias), while the second converts the resulting string into a INT64 hash.

By comparing the total number of rows in a group against the distinct count of these fingerprints, we can determine whether the proposed grain is correct and whether there are duplicates in the data.

This was a quick exercise but use this with care. Depending on your SQL implementation, data volumes and context, results may vary.

![](https://miro.medium.com/v2/resize:fit:700/0*r6BJhPYZrb7ivJg5 align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](http://notjustsql.com)*.*