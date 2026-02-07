---
title: "A quick walkthrough BigQuery Remote Functions"
seoTitle: "BigQuery Remote Functions: Quick Guide"
seoDescription: "Explore how BigQuery Remote Functions enable data processing using external resources with step-by-step guidance"
datePublished: Sat Mar 08 2025 22:16:09 GMT+0000 (Coordinated Universal Time)
cuid: cm80rkdic000009jp4rkq51l5
slug: a-quick-walkthrough-bigquery-remote-functions
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/vUxSIkqveu8/upload/9ddbbdc1ce0a99d8ab9b0c1e1a933e01.jpeg
tags: analytics, databases, google-cloud, sql, bigquery, gcp

---

In [a previous post](https://datawise.dev/a-quick-overview-of-bigquery-functions), I mentioned Remote Functions—a powerful way to send data from BigQuery to an external service for processing, including a Cloud Run function.

This is especially useful when SQL lacks built-in support for your specific needs, and writing a UDF isn’t an option (for example, if you need a highly specialized Python function).

Before building your own, check out [bigfunctions](https://unytics.io/bigfunctions/)—many common use cases have already been solved by others!

## What are remote functions in BigQuery?

These are a special type of function that delegates processing of input to an external resource, allowing us to:

* **send** **data** from BigQuery to Google Cloud Functions or other external services
    
* **process** **it** using a programming language
    
* **return results** to our query
    

## Why is that important?

A Google Remote function can encapsulate any kind of logic in major programming languages.

This opens the door to vast a ecosystem of libraries such at the Python packages.

Let’s look at a step-by-step example of creating a Remote Function.

## Step 1: Create the Cloud Run Function

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1741471414177/6d8b849d-737f-4efe-a3ab-a39f1dd24e96.png align="center")

## Step 2: Create a connection

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1741471757275/f7419114-e5fc-4feb-b080-184828d20a13.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1741471864886/3b677c91-3f43-4831-9374-e23ab82cb978.png align="center")

## Step 3: Set up permissions

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1741471928975/1ef3beac-2918-4766-b21e-68949299d7b5.png align="center")

## Step 4: Bind the connection with Cloud Run function

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1741471980691/6b5ce09d-a1b1-4603-9d23-48d7556013bd.png align="center")

## Test run

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1741472093181/dd455fb7-9653-41b5-a54a-87460190feee.png align="center")

*Found it useful? Subscribe to my Analytics newsletter at* [***notjustsql.com***](https://notjustsql.com/)*.*