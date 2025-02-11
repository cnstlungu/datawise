---
title: "Why you should use parentheses with AND & OR in SQL"
datePublished: Fri May 24 2024 04:44:38 GMT+0000 (Coordinated Universal Time)
cuid: clwk76saq000909mlak529uv8
slug: why-you-should-use-parentheses-with-and-or-in-sql
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/IiEFmIXZWSw/upload/0ca235f390d893093fb44bed2633272f.jpeg
tags: databases, google-cloud, sql, bigquery, data-engineering

---

If you filter the data in SQL with WHERE using multiple logical conditions tied with AND & OR, PLEASE use the parentheses them accordingly.

Because if you don't, your fellow team members are going to have a harder time understanding your intent.

You might also get unintended results based on how they are resolved:

`... operators with the same precedence are left associative. This means that those operators are grouped together starting from the left and moving right.`

AND [has a higher order of precedence](https://cloud.google.com/bigquery/docs/reference/standard-sql/operators#operator_precedence) than OR, therefore, in the example below:

`is_paid AND is_shipped OR customer_is_on_contract AND is_first_time_buyer`

is equivalent to

`( is_paid AND is_shipped) OR (customer_is_on_contract AND is_first_time_buyer)`.

It should also be noted that for comparison operators parentheses are required in order to resolve ambiguity since they are not associative like NOT/AND/OR.

![](https://miro.medium.com/v2/resize:fit:1400/0*XdwEb4cE_w8kHhcb align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](http://notjustsql.com)*.*