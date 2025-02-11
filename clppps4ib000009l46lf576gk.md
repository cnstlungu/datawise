---
title: "Does order of expressions in the WHERE clause matter?"
datePublished: Sun Dec 03 2023 16:46:01 GMT+0000 (Coordinated Universal Time)
cuid: clppps4ib000009l46lf576gk
slug: does-order-of-expressions-in-the-where-clause-matter
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/0aqJNZ5tVBc/upload/135a73de748611ac37eb11eb8dfb91c6.jpeg
tags: analytics, databases, google-cloud, bigquery, data-engineering

---

Does the order of expressions in a WHERE clause matter for performance?

So an interesting point found in a [Google Cloud blog post](https://cloud.google.com/blog/topics/developers-practitioners/bigquery-admin-reference-guide-query-optimization) was the fact that this expression order matters, with BigQuery assuming that the user has provided the best order of expressions in the WHERE clause, so it would not reorder expressions.

The recommendation given is to put the most selective expression first - basically, the one that narrows down the result set the most.

For testing it out, I've picked a ~200 million rows table (the publicly available `google_trends.international_top_terms`) .

The two scenarios to be tested were the ones presented in the same blog post - an exact match on a string and a wildcard lookup, then switching their order in the WHERE clause.

Now, the blog post is already more than 2 years old and some things might have changed, given I wasn't able to replicate the results very well.

The results have shown almost no difference between the two approaches (across several attempts), but another reason might be the table is just not big enough for me to see a difference.

![](https://miro.medium.com/v2/resize:fit:1400/0*SXbQmrErWonR7LYu align="left")

In any case, I'll keep this in mind next time I'm working with a very big table and check it out again.

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*