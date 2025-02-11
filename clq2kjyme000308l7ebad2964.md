---
title: "Using ARRAY_CONCAT_AGG() in BigQuery"
datePublished: Tue Dec 12 2023 16:40:42 GMT+0000 (Coordinated Universal Time)
cuid: clq2kjyme000308l7ebad2964
slug: using-arrayconcatagg-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/93x6yZautvA/upload/d5ae8f31d0f7ae0e9cc3fe587468f008.jpeg
tags: analytics, databases, google-cloud, sql, bigquery, data-engineering

---

If you're working with ARRAYS in BigQuery, you might need to combine two arrays into one at some point in time. That's why I want to showcase an interesting function - `ARRAY_CONCAT_AGG`.

What does it do? It's an aggregation function, it allows us to stitch together arrays in a particular group, yielding a concatenated array.

🔎 But watch out for:  
\- duplicates - it will not filter out duplicates for you  
\- NULL ARRAY is OK, but a NULL member of an ARRAY is not - you'll get an error ⁉

```sql
WITH example_table AS (
  SELECT [1, 2] AS array_column UNION ALL
  SELECT [3, 4] UNION ALL
  SELECT NULL UNION ALL
  SELECT [5, NULL, 6]
)
-- this will raise an ERROR because of the NULL in the last row
SELECT ARRAY_CONCAT_AGG(array_column) AS aggregated_array
FROM example_table
```

🥛+ 🍪 You can pair it with:  
\- ORDER BY to sort the INPUTS to the function (not the elements inside the array)  
\- LIMIT to keep only a specified number of input arrays

Let's see a practical example. Suppose our input data looks as follows.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702399012691/bc82a160-8f37-4977-bacb-80566f5e20bf.png align="center")

We'd like to combine offices by country into a single array (they are currently stored in one array per region).

```sql
WITH input_data  AS (
  SELECT 'US' AS country, [STRUCT('New York' AS city_name, 1000 AS staff_count), STRUCT( 'Boston' AS city_name, 500 AS staff_count) , STRUCT( 'Washington' AS city_name, 300 AS staff_count)   ] AS offices, 'US-East' AS region  
  UNION ALL 
  SELECT 'US' AS country, [STRUCT('Los Angeles' AS city_name, 700 AS staff_count) ,STRUCT('Denver' AS city_name, 400 AS staff_count)  , STRUCT('San Francisco' AS city_name, 250 AS staff_count)  ] AS offices, 'US-West' AS region
  UNION ALL 
  SELECT 'CA' AS country,  [STRUCT('Calgary' AS city_name, 400 AS staff_count) ,STRUCT('Vancouver' AS city_name, 1100 AS staff_count)  , STRUCT('Edmonton' AS city_name, 150 AS staff_count)  ] AS offices, 'CA-West' AS region 
  UNION ALL 
  SELECT 'CA' AS country,  [STRUCT('Quebec City' AS city_name, 200 AS staff_count) ,STRUCT('Montreal' AS city_name, 750 AS staff_count)  , STRUCT('Toronto' AS city_name, 800 AS staff_count)  ] AS offices, 'CA-East' AS region
  )
  SELECT 
  
    country, 
    ARRAY_CONCAT_AGG(offices) AS offices 
    
  FROM input_data

  GROUP BY country
```

Here's what the result would look like:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704891108534/7146c717-33b4-49b0-af54-fab9e81e6510.png align="center")

Thanks for reading!

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*