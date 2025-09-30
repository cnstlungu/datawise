---
title: "WITH expressions in BigQuery"
datePublished: Tue Sep 30 2025 05:38:06 GMT+0000 (Coordinated Universal Time)
cuid: cmg64mcv4000102jp2j0sb5mg
slug: with-expressions-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/GkinCd2enIY/upload/d3a3e22243bdd1ba959be7269ef16ffb.jpeg
tags: analytics, databases, google-cloud, sql, bigquery, data-engineering

---

So I recently discovered the WITH expression in BigQuery SQL.

Not to be confused with the WITH clause, which we use to define common table expressions (CTEs).

👉 What does a WITH expression do?  
It lets you define a series of variables, scoped to a single expression. Each variable can reference previously defined ones (and table columns), and in the end, the whole expression returns a result.

📌 Where could this be useful?  
Think back to the time before QUALIFY was supported. We often had to create an extra CTE just to filter with WHERE rn = 1 or for similar windowed calculations. When QUALIFY came, it saved us a bunch of boilerplate CTEs.  
Well, WITH expressions have the potential to help in the same way — but for non-window calculations.

When working with complex formulas, you can’t reference (within the same SELECT) a column you just defined. The usual workaround is to push it into another CTE — which works, but feels verbose. I still opted to do it since it's important that the code stayed readable and maintainable.  
Now WITH expressions give us a cleaner option and help avoid those 7-operand expressions. I, for one, plan on trying them out ASAP.

![No alternative text description for this image](https://media.licdn.com/dms/image/v2/D4D22AQEYGcsgW1-GOg/feedshare-shrink_1280/B4DZmREMcKJAAs-/0/1759075420579?e=1762387200&v=beta&t=Mwpk6vRASHgoM9J4QW87bwYlbf-JVBq7UqKCAzVfeIY align="left")

Has anyone here used them already? Any thoughts? Docs [here](https://cloud.google.com/bigquery/docs/reference/standard-sql/operators#with_expression).

*Found it useful? Subscribe to my Analytics newsletter at* [***notjustsql.com***](https://notjustsql.com/)*.*