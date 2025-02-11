---
title: "Cleaning up STRINGS in BigQuery"
datePublished: Wed Apr 24 2024 21:27:43 GMT+0000 (Coordinated Universal Time)
cuid: clvebt7ae00020amef47t9blm
slug: cleaning-up-strings-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/__ZMnefoI3k/upload/fbb56c2a25b80c649488765f453d4965.jpeg
tags: analytics, databases, google-cloud, sql, bigquery

---

Data is collected and processed in a number of ways, and it should come as no surprise that it's not always perfect.

Perhaps the most important thing you need to do before analyzing data is have a look at how it's presented and check for irregularities.

Before any sound analysis a great deal of attention needs to be paid to cleaning the data.

Take string columns for instance. In [hashtag#BigQuery, as with ot](https://www.linkedin.com/feed/hashtag/?keywords=bigquery&highlightedUpdateUrns=urn%3Ali%3Aactivity%3A7188500022613721089)her engines, there is a wealth of functions helping you to process strings, including:

\- TRIM/RTRIM/LTRIM for getting rid of the whitespace  
\- REPLACE to replace a substring with another one  
\- UPPER/LOWER/NORMALIZE etc to control casing  
\- SUBSTR/SUBSTRING to cut strings and so on.

The main goal here is to bring everything to a common denominator, being able to tell which observations belong together and which data can be considered "missing".

![](https://miro.medium.com/v2/resize:fit:1400/0*vKmmpl57wTjyWEds align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*