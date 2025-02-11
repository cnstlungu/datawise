---
title: "Easy with that SELECT DISTINCT!"
datePublished: Sat Jun 08 2024 17:42:55 GMT+0000 (Coordinated Universal Time)
cuid: clx6elg35000009lc1fhcftcx
slug: easy-with-that-select-distinct
canonical: https://www.notjustsql.com/p/easy-with-that-select-distinct
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1717869027576/32635a0b-4d29-487a-91c4-3373df54d44b.jpeg
tags: analytics, databases, sql, data-engineering, data-analytics

---

So you have to write a SQL query and after tirelessly working on it, you get more rows than you expected. It looks otherwise correct, but some of the records you see multiple times.

Now, while the temptation to just slap a DISTINCT in that final SELECT is enormous, don't succumb to it (yes I wrote this word).

Indiscriminate usage of DISTINCT might cover up a few problems with your query or can even come back to bite you.

### 1\. Bad join

It could be that one of your joins is incorrect or you might need, for example, an extra condition there.

Or you've unwillingly created a self-join like a.id = a.id 😁 Been there, done that.

### 2\. Incorrect grain

One of the tables you've retrieved data from has a finer granularity that you think, for example, multiple product variants that share the same id instead of just one product id per row.

Or you're getting multiple status updates throughout the lifetime of an order. Do you need to pick only one of these multiple rows, say the last status update?

Or you're trying to join month-level and day-level attributes together.

Do you need to aggregate or split one of the inputs to match the others?

### 3\. Are you working with nested data?

If you're working with nested data and proceed to unpack it i.e. UNNEST an ARRAY in BigQuery, you'll get the non-nested column repeated multiple times. Ensure you’re correctly processing the nested data as per your requirements.

### What should I do? How can I debug a problem with duplicates?

Thanks for reading Not just SQL! Subscribe for free to receive new posts and support my work.

* Pick a subset of data that you can simply analyze at a glance: a day, a single store, a product or one single order.
    
* Filter the data for just that. Are you getting the expected amount or rows? Is the granularity what you expected?
    
* Have a look at each table individually that you are using in your query.
    
* If you know an exact number of rows you should be seeing as output (e.g. total number of orders) you could comment out all the columns and put a SELECT COUNT(1) instead. Comment out the joined tables and add them back one by one. At what point in time does the COUNT result change for the worse?
    

If you still need to de-duplicate, say because the data is bad at the source (and you know it for a fact) or you receive multiple status updates but only want the last one - do so in an explicit manner, clearly showing how you are doing it and ideally explain in a short comment why you are doing it.

This could look like the following:

```sql
QUALIFY ROW_NUMBER() OVER (PARTITION BY order_id ORDER BY status_update_ts DESC)=1
```

If you're not familiar with QUALIFY and other ways to de-duplicate, check out the comprehensive [Medium article](https://medium.com/google-cloud/deduplication-in-bigquery-tables-a-comparative-study-of-7-approaches-f48966eeea2b) about the many ways you can de-duplicate and their pros & cons.

Happy querying!

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://notjustsql.com)*.*