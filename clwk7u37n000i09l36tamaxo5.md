---
title: "Using the bq CLI utility with BigQuery"
seoTitle: "BigQuery bq CLI: Queries, Tables, and IAM from Terminal"
seoDescription: "The bq command-line tool lets you run queries, manage tables, load data, and view IAM policies in BigQuery without the Console."
datePublished: Fri May 24 2024 05:02:45 GMT+0000 (Coordinated Universal Time)
cuid: clwk7u37n000i09l36tamaxo5
slug: using-the-bq-cli-utility-with-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/xbEVM6oJ1Fs/upload/9f10de7734d244d209aa44dd756b644d.jpeg
tags: analytics, google-cloud, sql, bigquery, data-engineering

---


Remember that in additional to the Cloud Console GUI or client libraries, you can also perform BigQuery tasks using the `bq` command-line interface.

It's included with the gcloud SDK and once you have logged in, you can perform a number of operations such as:  
\- run queries against BQ  
\- create, copy and delete tables  
\- load data into tables  
\- view IAM policies for a BQ asset and much more

How I've used it until now:  
\- [impersonate service accounts](https://hashnode.com/post/clw922i8y00010al7d4jg0mx9)  
\- perform operations that are/were not supported in the SQL interface, such as [copying partitions between tables](https://hashnode.com/post/clna9vnqg000909ju7efcgbv3)

Any other interesting ways you're using the bq cli tool?

![](https://miro.medium.com/v2/resize:fit:1400/0*VvVN8Y1vXzRvhdbN align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](http://notjustsql.com)*.*

---

*Enjoyed this? Here are some related articles you might find useful:*

- [Using GCP Cloud Functions in Data Engineering](https://datawise.dev/using-gcp-cloud-functions-in-data-engineering)
- [What are GCP Cloud Workflows and how can they help you as a Data Engineer](https://datawise.dev/what-are-gcp-cloud-workflows-and-how-can-they-help-you-as-a-data-engineer)
- [Loading data from Google Cloud Storage into BigQuery using Cloud Workflows](https://datawise.dev/loading-data-from-google-cloud-storage-into-bigquery-using-cloud-workflows)
- [Scheduled queries in BigQuery](https://datawise.dev/scheduled-queries-in-bigquery)
