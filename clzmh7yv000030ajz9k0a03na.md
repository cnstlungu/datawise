---
title: "Dynamically extracting JSON data in BigQuery"
datePublished: Fri Aug 09 2024 09:00:08 GMT+0000 (Coordinated Universal Time)
cuid: clzmh7yv000030ajz9k0a03na
slug: dynamically-extracting-json-data-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/sXiVEKjPcSA/upload/73947919856378d94489009f54baff48.jpeg
tags: databases, google-cloud, sql, bigquery, data-engineering

---

I was asked today about dynamically extracting key-value pairs from heterogeneous JSON-like strings in BigQuery SQL and I've remembered this interesting approach I've seen a while ago.

It leverages regular expressions, one of everyone's favorites, I know.

This allows extraction of key-value pairs from each JSON-like string, even if they are don't look the same.

Kudos to someone on Stack Overflow where I've first seen it.

Pretty sure the regex can be streamlined, but that's as much me feat. GPT could do today.

PS. If we're talking about JSON datatype, you can transform it to JSON-like STRING with TO\_JSON\_STRING() and do the same thing.

![](https://miro.medium.com/v2/resize:fit:1400/0*fRHBrsGhHg1b0FjQ align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://notjustsql.com)*.*