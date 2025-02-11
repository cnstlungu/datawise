---
title: "Scheduled queries in BigQuery"
datePublished: Sat Sep 02 2023 22:05:58 GMT+0000 (Coordinated Universal Time)
cuid: clm2kp7tx000608l7ecck8cqc
slug: scheduled-queries-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/FoKO4DpXamQ/upload/7d2a2f789ad8906f89fed80dfbbeeb3b.jpeg
tags: analytics, google-cloud, sql, bigquery

---

### What are Scheduled Queries?

Scheduled Queries in BigQuery allow users to run SQL tasks on a predefined, automated schedule.

Instead of manually initiating a query each day or week, BigQuery can do it for you. This is perfect for light orchestration of repetitive data transformations, updates, and regular reporting tasks.

### Creating a Scheduled Query manually

A scheduled query can be created manually using the **Schedule button** in the Query window.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693691084862/198e32a7-53d4-4765-979d-11c81673e48e.png align="center")

A dialog box is presented where we are prompted to provide the following information:

* a name for the scheduled query
    
* a scheduling option or the option to run it manually (on demand)
    
* start date and end date for which this query would run
    
* optionally, a destination dataset and table for the query result (including the possibility of adding a partitioning field)
    
* region selection
    
* encryption options
    
* principal (user or service account) to run the query under
    
* write disposition, in order words what to do with the contents already in the table: keep (and append new data) or overwrite (and replace with the new data)
    
* notification options
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693691127706/ee19eb2f-4118-461a-9599-c72e15556421.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693691161465/417ed50c-d8c8-4a01-8c18-499ce455b0c6.png align="left")

### Creating a scheduled query using Terraform

A schedule can also be created using Terraform, as per the following example.

This option provides a subset of options from the manual method - at the time of writing, for example, the write disposition cannot be set up here.

```bash
variable "envConfig" {

    type = map(object({
        project_id = string
        service_account_name = string
    }))
}

variable "config" {
    type = map(object({
        name = string
        query = string
        destination_table_name_template = string
    }))
}
```

```bash
resource "google_bigquery_data_transfer_config" "query_config" {
    for_each = var.config
    display_name = each.value["name"]
    location = "europe"
    data_source_id = "scheduled_query"
    schedule = "every saturday 05:00"
    destination_dataset_id = "learning"
    params = {
        destination_table_name_template = each.value["destination_table_name_template"]
        write_disposition = "WRITE_APPEND"
        query = each.value["query"]
    }
    service_account_name = var.envConfig["dev"].service_account_name
    project = var.envConfig["dev"].project_id
}
```

### Creating a Scheduled Query using the API

It's also possible to create a scheduled query using one of the BigQuery APIs or the bq CLI command - check the GCP documentation [here](https://cloud.google.com/bigquery/docs/scheduling-queries#python).

### Viewing scheduled queries

Viewing the scheduled query can be done by Accessing the 'Scheduled queries' option in the BigQuery subgroup.

It will display a list of queries, their schedule, region, destination (if any) and next run time.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693691948354/67ee35fa-6b2e-46cb-86d3-19d3f5b9e00e.png align="center")

Click on a particular query would present a Run history and its output. There is also an option for scheduling a backfill (which we can use for a Manual Run).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693692018427/94436650-f7a0-44ae-8890-37b9fcace1d5.png align="center")

Clicking on the **Configuration** tab would display the configurations used to create the query.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693692148191/aa35bc83-9ad5-475d-8d9c-987d1542189a.png align="center")

In conclusion, BigQuery Scheduled queries can be a useful tool in your toolset, as a quick and easy way to do light orchestration of SQL tasks.

Thanks for reading!

---

🚀 Delving into BigQuery, Google Cloud and Analytics? Stay connected with me for valuable insights, handy tips, and strategies to effortlessly traverse the vast universe of cloud computing and data analytics!

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*