---
title: "Why you should think twice before UNNESTing arrays or date intervals"
datePublished: Mon Jun 09 2025 21:17:43 GMT+0000 (Coordinated Universal Time)
cuid: cmbplfgs8000002l5abq9730e
slug: why-you-should-think-twice-before-unnesting-arrays-or-date-intervals
canonical: https://www.notjustsql.com/p/why-you-should-think-twice-before
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1749669518998/e83a7529-3787-4993-a114-c30602ad09d0.jpeg
tags: analytics, databases, sql, bigquery, data-engineering

---

If you ever work with terabyte-scale data, try to avoid unnecessary unnesting/unpacking arrays and date ranges. If you have no choice, materialize the unnested result and partition and cluster it accordingly in preparation for any further joins.

With that bold statement out there, here’s a BigQuery lesson drawn from real-world experience.

Imagine an SCD-2 table with tens of millions of rows containing product data.

For particular subintervals (even individual days) of the \[valid\_from, valid\_to) period, we need to set some attributes (think: marking that the product is on sale, or is getting ready to be discontinued).

The simple and straightforward solution here would be to unpack the intervals with something like UNNEST(GENERATE\_DATE\_ARRAY(valid\_from, valid\_to)). Joining with a date dimension would work in a similar fashion.

This means that it is easy to now look up these attributes at (grain + valid\_date).

But now we could be talking about several billion rows. Which you might join with other big tables.

The issues with this approach are quite obvious. Say we have a two-year interval. Unpacking this period would mean having 730 rows instead of one, while a majority of them would just be repeated data — there’s no actual change, just some spot changes for individual days or subintervals.

We can of course go ahead and compact this data back using an algorithm like the one I presented [in one of my previous posts](https://datawise.dev/compacting-date-intervals-in-bigquery), but regardless of whether we do that or not, the whole processing would be incredibly expensive and inefficient.

So, is there a solution here? Sometimes there might be.

Say for the two-year interval \[2021-01-01, 2023-01-01\], we’d need to mark the subperiod \[2021-04-15, 2021-05-15\] as the period when the product is on sale.

This data can be accurately expressed as the following intervals:

\[2021-01-01 → 2021-04-15),

\[2021-04-15 → 2021-05-15),

\[2021-05-15 → 2023-01-01).

So in fact, we’re splitting the intervals into smaller subintervals based on what was true at each moment. Instead of unpacking and getting hundreds of records, we need only 3. I’ve illustrated this approach [in another previous post](https://datawise.dev/practical-bigquery-joining-temporal-tables).

Such a difference in cardinality has deep performance implications, allowing us to process data way more efficiently.

While this might be an unusual corner case, my initial opinion stands — if you can get away without UNNESTing your array or unpacking a date interval, you’ll manage to keep cardinality in check and save a lot of processing power.

If there’s no way around it for your particular case, at the very least, materialize the result (I know, it’s going to be a lot of storage) and tailor the partitioning and clustering according to the querying (especially joining with other big+ tables) downstream.