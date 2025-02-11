---
title: "Rounding Timestamps in BigQuery"
seoTitle: "Rounding Timestamps in BigQuery"
seoDescription: "Practical exercise on rounding timestamps in BigQuery SQL"
datePublished: Sun Mar 26 2023 21:09:49 GMT+0000 (Coordinated Universal Time)
cuid: clfpw8pur000209jy97zpe92c
slug: rounding-timestamps-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/UAvYasdkzq8/upload/38dba26f272d7841f5473765fec670ba.jpeg
tags: sql, bigquery, gcp

---

Have you ever encountered a situation where you would need to round a timestamp to the nearest second, 5 seconds or minute? While rounding a number is trivial, it's a little bit less straightforward when dealing with timestamps.

Let's consider the following input data.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679863892370/7b766b6c-abd0-4f27-851a-852bfe7d590a.png align="center")

We have our *event\_times* that are at milliseconds-level grain. To round the times to the nearest granularity we'd like, we can use a combination of *UNIX\_MILLIS* and *TIMESTAMP\_MILLIS.*

The steps are as follows:

* Transform the timestamp into milliseconds since Unix epoch (that is, number of milliseconds that have passed since January 1st, 1970) with *UNIX\_MILLIS*
    
* Divide that number by your target grain in milliseconds i.e. 1000 for 1 second or 60000 for 1 minute
    
* *CAST* that number to an INT64
    
* Multiply that number by your target grain (the number from above) i.e. 1000 for 1 second or 60000 for 1 minute
    
* Transform it back to a timestamp using *TIMESTAMP\_MILLIS*
    

```sql
SELECT 

event_time,
UNIX_MILLIS(event_time) AS epoch_milliseconds,
TIMESTAMP_MILLIS( CAST(UNIX_MILLIS(event_time) / 1000 AS INT64) * 1000) AS nearest_second,
TIMESTAMP_MILLIS( CAST(UNIX_MILLIS(event_time) / 5000 AS INT64) * 5000) AS nearest_5seconds,
TIMESTAMP_MILLIS( CAST(UNIX_MILLIS(event_time) / 60000 AS INT64) * 60000) AS nearest_1minute,
TIMESTAMP_MILLIS( CAST(UNIX_MILLIS(event_time) / 300000 AS INT64) * 300000) AS nearest_5minutes,

FROM input_data
```

Upon executing this query, the following results are produced:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679864608020/8e9c0694-649a-486e-aed3-4590a6302667.png align="center")

The functions presented above and others relevant to working with timestamps are presented in the [documentation](https://cloud.google.com/bigquery/docs/reference/standard-sql/timestamp_functions).

Thanks for reading and enjoy working with BigQuery!

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*