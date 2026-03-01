---
title: "NATURAL JOIN in SQL"
seoTitle: "SQL NATURAL JOIN Explained: Auto-Join on Matching Columns"
seoDescription: "NATURAL JOIN automatically joins tables on columns sharing the same name and datatype, with no explicit condition needed."
datePublished: Thu Jun 20 2024 06:00:25 GMT+0000 (Coordinated Universal Time)
cuid: clxmus99000060ajs1dfi2y2z
slug: natural-join-in-sql
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/D9inTE660po/upload/139a597814d5e2104ad2189b71f3c899.jpeg
tags: databases, sql, bigquery

---

Another lesser known JOIN - the natural join. But maybe the NATURAL JOIN is not as obscure after all, since it has its own keyword, at least in a couple of [S](https://www.linkedin.com/feed/hashtag/?keywords=sql&highlightedUpdateUrns=urn%3Ali%3Aactivity%3A7205871620790317056)QL dialects - see PostgreSQL portrayed below (sorry, it's not supported in BigQuery, but it does recognize it).

So what's special about it? Well, it joins the tables based on columns that have the same name (and datatype) in the two tables. That is, we don't need to specify any join conditions.

Watch out because if there are no columns with the same name and datatype, it defaults to a Cartesian product is produced (which is what CROSS JOIN does).

![](https://miro.medium.com/v2/resize:fit:1400/0*Zjp2-l66WIDEsIdN align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://notjustsql.com)*.*

---

*Enjoyed this? Here are some related articles you might find useful:*

- [Self-joins in SQL](https://datawise.dev/self-joins-in-sql)
- [Anti-joins in SQL](https://datawise.dev/anti-joins-in-sql)
- [SEMI-JOINS in SQL](https://datawise.dev/semi-joins-in-sql)
- [NON-EQUI joins in SQL](https://datawise.dev/non-equi-joins-in-sql)
