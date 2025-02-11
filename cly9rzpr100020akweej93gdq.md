---
title: "Query parameters in BigQuery"
datePublished: Sat Jul 06 2024 07:00:56 GMT+0000 (Coordinated Universal Time)
cuid: cly9rzpr100020akweej93gdq
slug: query-parameters-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/KFF42HA6Oug/upload/809dea43b89343e97013c4f160372192.jpeg
tags: analytics, databases, google-cloud, sql, bigquery

---

Query parameters in BigQuery. You need to know about them if you're constructing queries based on user input. What do they do?

They can help secure your query against SQL injection and can be recognized by the @ (for named usage) and ? (for positional usage).

Unlike variables, with whom we should not confound them, one cannot use them in the console (web IDE), but only with bq command line interface, API or client libraries.

You can ✅ :  
\- use parameters for expressions  
\- provide a datatype for the query parameter or omit it with STRING as default  
\- use complex types such as ARRAY or STRUCT

But you cannot ❌ :  
\- pass parameters as column or table names  
\- use positional AND named parameters at the same time

![](https://miro.medium.com/v2/resize:fit:700/0*qu2_npQ8PXWZUXaA align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://notjustsql.com)*.*