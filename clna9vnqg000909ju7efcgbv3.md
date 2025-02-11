---
title: "Swapping Partitions in BigQuery"
datePublished: Tue Oct 03 2023 12:04:55 GMT+0000 (Coordinated Universal Time)
cuid: clna9vnqg000909ju7efcgbv3
slug: swapping-partitions-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/YEWvMidcKkg/upload/454938cba54f35773d7e049057cb0f56.jpeg
tags: sql, bigquery, gcp

---

A few years back, when working on SQL Server projects, I often utilized the ALTER TABLE SWITCH partition between staging and target tables. This left me pondering—could a similar functionality be achieved in BigQuery? 🤔

BigQuery facilitates copying a partition to another table using the bq cp command:

```bash
bq cp -f 'project:dataset.source_table$your_partition' 'project:dataset.target_table$your_partition'
```

🧪 Example Scenario 🧪

Imagine a staging table, where we extract the delta from a source table (based on the last entry seen in the target table), and MERGE it into the target table.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696334449332/8301c78e-b3e0-4efc-bcb0-11976434a170.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696334464272/3f973cfd-175e-40cc-b42f-69a374b13d45.png align="center")

Instead, we can craft a short script to copy delta partitions (new + changed, if any) into the target table, bypassing the need for MERGE altogether! This generates COPY jobs as opposed to QUERY jobs.

```bash
#!/bin/bash

# Check if the correct number of arguments is provided
if [[ "$#" -ne 2 ]]; then
    echo "Usage: $0 <start_date> <end_date>"
    exit 1
fi

# Define the project and dataset names
PROJECT="***********"
DATASET_SOURCE="learning.data_source_staging"
DATASET_DEST="learning.data_source"

# Assign start date and end date from input arguments
START_DATE=$1
END_DATE=$2

# Loop through the dates from START_DATE to END_DATE
for date in $(seq -w $START_DATE $END_DATE); do
  # Echo a message indicating the partition being swapped
  echo "Swapping partition $date"
  
  # Run the bq cp statement
  bq cp -f "${PROJECT}:${DATASET_SOURCE}\$$date" "${PROJECT}:${DATASET_DEST}\$$date"
done
```

Once this executes, we will have copied the partitions from the staging table to the target table using the `bq cp` command.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696334598228/18b3b452-a9fa-49b8-a59d-8bb91758f6c5.png align="center")

We can confirm that all the partitions have been loaded properly and see the list of COPY jobs in the job history tab.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696334649566/7c5a3ccd-838d-46de-bb02-ad504b895ef1.png align="center")

Also, don’t forget—leveraging the INFORMATION\_SCHEMA PARTITIONS view can assist in constructing even more advanced functionalities.

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*