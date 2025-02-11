---
title: "Transactions in BigQuery"
datePublished: Thu May 09 2024 20:57:23 GMT+0000 (Coordinated Universal Time)
cuid: clvzqbyzf00010al9ejwfcf67
slug: transactions-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/4vMfb8srdTQ/upload/f9b64bbefe819d5a89929fb17c6173a8.jpeg
tags: analytics, database, google-cloud, sql, bigquery, gcp

---

For a long time I didn't even know transactions existed in BigQuery. How are they useful?

Say you are performing a number of operations that you would like to succeed in full (so all steps are successful) or be aborted entirely (reverting to the previous state), basically ALL or NOTHING.

In case an error occurs in any of the operations inside the transaction block (BEGIN TRANSACTION -&gt; COMMIT TRANSACTION), all the operations are rolled back, with the state being reverted to what it was before.

The docs point out that use cases for transactions could include:  
\- changes to multiple tables at ones  
\- changes to one table in stages, based on some intermediate calculations we perform

In the example below, we wanted to perform another operation after inserting a row in the table, but upon encountering an error, that change is reverted as well, leaving us with the state we had before running this code.

![](https://miro.medium.com/v2/resize:fit:1400/0*KDfNxqpBZSvwL63E align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](http://notjustsql.com)*.*