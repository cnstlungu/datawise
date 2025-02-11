---
title: "Pay attention to this when UNNESTING in BigQuery"
datePublished: Thu Oct 19 2023 22:30:51 GMT+0000 (Coordinated Universal Time)
cuid: clnxra8pf000109la9lxd343d
slug: pay-attention-to-this-when-unnesting-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/dnGgAIRNnsE/upload/9049fa6dd2688042be29866312924f1d.jpeg
tags: google-cloud, sql, bigquery

---

Here's a common confusion that I encounter while working with ARRAYs in BigQuery. This can lead to wrong queries in some situations. Consider the following two snippets:

```sql
FROM table,
UNNEST(repeated_column) AS single_item
```

versus

```sql

FROM table
LEFT JOIN UNNEST(repeated_column) AS single_item
```

They are very different.

In the first, the comma ',' essentially behaves like a CROSS JOIN, pairing each row of the table with every element of the array in its repeated\_column.

In the second, we're using a LEFT JOIN, ensuring retention of all rows in the table, even those without a value in the repeated\_column.

How is this important, you'll ask. Consider the following case.

Imagine you'd need to compute the number of unique banks a person is a customer of in the example below.

![](https://miro.medium.com/v2/resize:fit:1400/0*r9ZlbWJqfbicE1Ws align="left")

A person can be a customer of one, multiple or no bank at all. This becomes important if a customer has no accounts, using UNNEST joined with the comma (CROSS JOIN) would exclude these entries.

```sql
SELECT 
  person_id, 
  COUNT(DISTINCT bank_account.bank_name) AS count_distinct_banks 
FROM input_data,
UNNEST(bank_accounts) AS bank_account 

GROUP BY person_id
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697754402590/7478ce3f-5cb5-4a83-941b-e52380afee44.png align="center")

If we want to keep these entries, we'd need to use LEFT JOIN.

```sql
SELECT 
person_id, 
COUNT(DISTINCT bank_account.bank_name) AS count_distinct_banks 
FROM input_data

LEFT JOIN UNNEST(bank_accounts) AS bank_account 
GROUP BY person_id
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697754448042/71c25019-9c7f-4d0b-8de9-ac73c1c3f092.png align="center")

In this case, the first approach would miss out on the people without a bank account, while the second would include them. Quite a big difference in query results if you ask me.

Have fun writing good SQL!

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*