---
title: "The power of BigQuery INFORMATION_SCHEMA views"
seoTitle: "Unlocking BigQuery: Mastering INFORMATION_SCHEMA Views"
seoDescription: "Dive into BigQuery's INFORMATION_SCHEMA views to analyze datasets, optimize storage costs, and build dynamic queries."
datePublished: Mon Sep 25 2023 21:33:09 GMT+0000 (Coordinated Universal Time)
cuid: clmzenloq000008l69o4m0feh
slug: the-power-of-bigquery-informationschema-views
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/FKqxZ58bVjU/upload/2603040576bbbef17a8cdf343895a01e.jpeg
tags: analytics, sql, bigquery, gcp

---

In one of the [previous posts about BigQuery labels](https://hashnode.com/post/clmze56oz000308ld27v2crzo), I provided an example showcasing the usage of the INFORMATION\_SCHEMA JOBS view when analyzing query statistics per label.

Now what are these views? These are system-generated views that provide metadata about your datasets, tables, columns, jobs, partitions, constraints and more.

Just wanted to highlight that INFORMATION\_SCHEMA view (JOBS included) can do much, much more than that.

Look into your table storage costs, query resource consumption, build dynamic queries, and leverage partition metadata for incremental pipelines - all of this can benefit from the INFORMATION\_SCHEMA views.

Let's look at a couple of interesting use cases.

## JOBS

JOBS is one of the most powerful views when you’re interested in the queries run in that project. It can provide information about:

* slot time used
    
* runtime
    
* bytes processed and billed
    
* referenced tables
    
* errors if any and so much more!
    

```sql
SELECT 

creation_time, 
job_type, 
query, 
total_bytes_billed, 
total_bytes_processed, 
total_slot_ms, 
referenced_table.table_id AS referenced_table_name

FROM `region-eu`.INFORMATION_SCHEMA.JOBS,
UNNEST(referenced_tables) AS referenced_table
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695677090320/8c4dbcdd-b557-44e2-918d-095c880f6646.png align="center")

## **COLUMNS**

This view contains information about columns, such as:

* tables where they reside
    
* data types
    
* whether they are nullable or not
    
* default values if any
    

Need a dynamic UNPIVOT? Fetch the column names dynamically using this view.

```sql
DECLARE myunpivot STRING;
SET myunpivot = (
  SELECT CONCAT('(', STRING_AGG( column_name, ','), ')'),
From(
SELECT column_name FROM learning.INFORMATION_SCHEMA.COLUMNS
where table_name ="Customer_Data" 
and column_name not in("CustomerId")  ));

EXECUTE IMMEDIATE format("""
SELECT * FROM
(
  SELECT * FROM learning.Customer_Data
)
unpivot
(
  value 
  FOR keys in %s
)
""", myunpivot);
```

FROM:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695677265843/f7073ffc-91f3-4d32-948e-5bc0f8af2524.png align="center")

TO:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695677293199/6351e972-d536-4ec5-a148-468ec3ffd37e.png align="center")

## CONSTRAINT COLUMN USAGE

If you’re interested in column usage in constraints (newly added BigQuery feature), there is this dataset-level view, showcasing which constraints are applied to columns.

```sql
SELECT * EXCEPT(table_catalog, constraint_catalog) 

FROM testing.INFORMATION_SCHEMA.CONSTRAINT_COLUMN_USAGE;
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695677390758/0748ae82-4bd4-4e99-a101-7479a79a1096.png align="center")

## TABLE STORAGE

Looking to dive into table storage, including physical and logical storage, so you can estimate your costs? Use one of the table storage views (per project or region, as below).

```sql
SELECT * FROM region-eu.INFORMATION_SCHEMA.TABLE_STORAGE;
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695677435416/baace21f-a3ff-40b1-8313-a661faf912cc.png align="center")

## But there's more!

* Building an incremental pipeline and you’d like information about the last time a Partition has been modified? There’s the PARTITIONS view.
    
* Looking to find object access grants? There’s OBJECT\_PRIVILEGES
    
* Want to see a list of Table Snapshots? There is a view for that too.
    
* Be sure to check the [BigQuery documentation](https://cloud.google.com/bigquery/docs/information-schema-table-storage) for the latest list of INFORMATION SCHEMA views you can use
    

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*