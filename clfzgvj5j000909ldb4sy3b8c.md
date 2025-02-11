---
title: "Using BigQuery Time Travel"
datePublished: Sun Apr 02 2023 13:57:22 GMT+0000 (Coordinated Universal Time)
cuid: clfzgvj5j000909ldb4sy3b8c
slug: using-bigquery-time-travel
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/W9jfKmGYb1Q/upload/80070b90ae991df1882328807ba0d6e7.jpeg
tags: analytics, sql, bigquery, business-intelligence, data-warehousing

---

In this practical BigQuery exercise, we’re going to look at [BigQuery Time Travel](https://cloud.google.com/bigquery/docs/time-travel) and see how it can help us when working with data. It’s not as powerful as Marty McFly’s DeLorean in Back to the Future (nobody knows what your future data will look like), but a useful tool in our toolset nevertheless.

First of all, what is BigQuery Time Travel? It allows for retrieving the state of a particular table at a given point within a time window, which is set by default to 7 days.

Let’s have a look at an example. At 11:00 AM we’ll create the following table.

```sql
CREATE TABLE `learning.test_time_travel` AS 


SELECT 1 as id, 'abc' as value

UNION ALL

SELECT 2 as id, 'def' as value
```

![](https://miro.medium.com/v2/resize:fit:349/1*cZfOLF_wBBoCVhQg1gmZQQ.png align="left")

Then, several minutes later, we make some changes to that table, say, insert a row.

```sql
INSERT INTO `learning.test_time_travel`

SELECT 3 AS id, 'hij' AS value
```

![](https://miro.medium.com/v2/resize:fit:338/1*sofLfH8dZICkanf_P1oYdw.png align="left")

We can now confirm that we have the extra row. But what if we’d like to query the table as of earlier?

```sql
SELECT * FROM learning.test_time_travel

FOR SYSTEM_TIME AS OF TIMESTAMP('2023-04-02 11:00:00.000 UTC')
```

![](https://miro.medium.com/v2/resize:fit:489/1*ijSVTforfdm9_DXl0wWVWg.png align="left")

Using the approach above we can query the table at any particular point in the time travel window, set by default to 7 days, but configurable to be between 2 and 7 days.

## Changing the time travel window

The time travel window is set at a dataset level, so affects all the tables in that dataset. The default time travel windows (7 days) can be overridden either at [dataset creation time](https://cloud.google.com/bigquery/docs/datasets#sql) or on [an existing dataset.](https://cloud.google.com/bigquery/docs/updating-datasets#update_time_travel_windows)

```sql
CREATE SCHEMA my_project.my_dataset
  OPTIONS (
    max_time_travel_hours = your_number_of_hours_here
);
```

```sql
 ALTER SCHEMA my_dataset
    SET OPTIONS(
      max_time_travel_hours = your_number_of_hours_here
);
```

## Practical considerations

The **FOR SYSTEM\_TIME AS OF** clause comes after the table you’d like to apply Time Travel to, so a join query would look as follows.

```sql
SELECT t1.*, t2.other_value 
FROM learning.test_time_travel t1 FOR SYSTEM_TIME AS OF TIMESTAMP('2023-04-02 11:00:00.000 UTC')
FULL OUTER JOIN learning.other_test_table  t2 FOR SYSTEM_TIME AS OF TIMESTAMP('2023-04-02 13:41:00.000 UTC') on t1.id = t2.id
```

Also, if you’d like to copy the table at a particular point in time, that can be done using the **bq** utility (part of the **gcloud CLI**).

```sql
bq cp learning.test_time_travel@1680433200000 learning.test_time_travel_backup
```

Note that the timestamp there is the UNIX epoch in milliseconds, which can be obtained as follows.

```sql
SELECT UNIX_MILLIS(TIMESTAMP('2023-04-02 11:00:00.000 UTC'))
```

## Conclusion

In this short practical exercise, we’ve looked at BigQuery Time Travel, a very handy tool to aid us in querying previous states of a particular table. I found it very helpful when debugging data pipelines.

Thanks for reading and stay tuned for more practical BigQuery tips.

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*