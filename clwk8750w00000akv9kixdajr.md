---
title: "What are GCP Cloud Workflows and how can they help you as a Data Engineer"
datePublished: Fri May 24 2024 05:12:54 GMT+0000 (Coordinated Universal Time)
cuid: clwk8750w00000akv9kixdajr
slug: what-are-gcp-cloud-workflows-and-how-can-they-help-you-as-a-data-engineer
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/_QoAuZGAoPY/upload/7a27e7bad2c1068d2a7313d383160ba3.jpeg
tags: analytics, google-cloud, bigquery, data-engineering

---

A reminder that you don't necessarily need Airflow / Composer to orchestrate data in and out of BigQuery. If your workflows are not that complex or numerous, take a look at Google Cloud Workflows.  
  
It's a serverless orchestration engine, with good integration with other GCP services, but you can also call external APIs.  
  
Some advantages I see:  
\- serverless, no servers to manage  
\- your workflows stored as code, manage Infra as Code with Terraform  
\- interact with external APIs  
\- good connectors to interact with other GCP services  
\- straightforward pricing: at the time of writing: 5k steps free per month, 0.01 USD per 1k steps after, external API call are priced separately (2k/mo free, 0.025 USD per 1k after)  
  
I've used it before to load data from Google Cloud Storage into BigQuery tables on a schedule and perform other simple tasks. It gets the job done with no fuss. You can of course schedule the Workflow to run with Cloud Scheduler.  
  
See [my previous post](https://datawise.dev/loading-data-from-google-cloud-storage-into-bigquery-using-cloud-workflows) for a short walk through showcasing how BQ and Workflows play together.

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](http://notjustsql.com)*.*