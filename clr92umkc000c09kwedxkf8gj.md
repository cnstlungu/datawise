---
title: "Using RANGE in Window Functions in BigQuery"
datePublished: Thu Jan 11 2024 10:39:12 GMT+0000 (Coordinated Universal Time)
cuid: clr92umkc000c09kwedxkf8gj
slug: using-range-in-window-functions-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/jUCQRQeRs3k/upload/5927fa0f6c7e32d62d5b62dfae90a29e.jpeg
tags: analytics, google-cloud, sql, bigquery, data-engineering

---

On [my previous post about computing a cumulative sum](https://datawise.dev/computing-a-cumulative-sum-in-bigquery) in BigQuery I've got a question regarding the RANGE in the row\_range specification of a window function. I've realized I never used it before. So I've decided to see what it's about.

So how does using RANGE inside an OVER() block differ from using ROWS?

First, it bears noting that unlike ROWS, which uses physical rows representation (previous row, next row etc) in a window, RANGE uses logical (previous value, next value), so that makes it quite useful in some situations.

Let's imagine the following scenario:

We have a group of athletes that compete in a running contest. We would like to compare each athlete's time to their peers - but we'll define a peer as someone who is born anywhere between the year before and the year after the athlete was. So for someone born in 1992, we would like to compute the average of athletes born in '91, '92 and '93 for comparison.

How will this be achieved?

We'll use the AVG aggregation function with a window function call, ORDER BY birth\_year and set up a RANGE BETWEEN 1 PRECEDING year and 1 FOLLOWING year. This way, for our athlete born in '92, the average will be computed by including all athletes born in 1991, 1992, 1993.

To illustrate why the ROWS would not work here, look at the results for 1991. Since there's two athletes born in 1991, the ROWS clause would include only the previous row (also born in 1991) and the next row (born in 1992), thus missing the mark. Check the result in neighbours\_average vs neighbours\_average\_wrong.

![](https://miro.medium.com/v2/resize:fit:1400/0*yjBDqR8itW-EDS22 align="left")

RANGE comes with a limitation though - you can only order by a single numerical column.

Hope this was interesting!

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*