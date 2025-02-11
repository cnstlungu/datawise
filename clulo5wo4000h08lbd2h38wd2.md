---
title: "Extract all pattern occurrences in BigQuery"
datePublished: Thu Apr 04 2024 20:08:12 GMT+0000 (Coordinated Universal Time)
cuid: clulo5wo4000h08lbd2h38wd2
slug: extract-all-pattern-occurrences-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/GZMjMukr5zU/upload/285d275f0056de8ab7823cb2232a8b66.jpeg
tags: databases, google-cloud, sql, bigquery, data-engineering

---

If you ever need to extract information based on a pattern in a BigQuery string, check out the `REGEXP_EXTRACT_ALL` function.

This will return an array of all the occurrences matching the specified regular expression.

With regards to the pattern itself, I typically use a representative example with a regex debugger like [regex101](https://regex101.com/).

Worth noting that it has a limitation - it would only work with a single regex capture group, so you can't match multiple patterns at the same time.

![](https://miro.medium.com/v2/resize:fit:1400/0*Fxorjdvu_k44mtja align="left")

*Found it useful? Check out to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*