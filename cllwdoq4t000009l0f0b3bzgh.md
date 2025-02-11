---
title: "Row-level access security in BigQuery"
datePublished: Tue Aug 29 2023 14:03:01 GMT+0000 (Coordinated Universal Time)
cuid: cllwdoq4t000009l0f0b3bzgh
slug: row-level-access-security-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/5tmItJfHkIc/upload/5fe4e2b9cff1538de866187268de5c9a.jpeg
tags: analytics, security, google-cloud, bigquery

---

Whether you're an experienced data engineer or just embarking on your cloud data adventure, prioritizing security is crucial.

Here's a quick tour of BigQuery's row-level security features.

Suppose you have the following BigQuery table. Each sales representative should only have access to the data for the country they are catering to.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693317467077/4e5ee276-aa5e-435e-9574-97e1f2c78d28.png align="center")

Let's define a **Row-level access policy**.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693317519962/9a20bfb1-2f3d-42eb-8b87-9068095426e5.png align="center")

This service account would now only be able to see rows where the country is the US or UK.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693317556024/7681a211-4b58-46cf-9776-2204283dc884.png align="center")

Other users (without a Row-level access policy) would see the following:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693317588690/0aad0030-f5ab-41c6-a2a9-3e1948b9b2bf.png align="center")

**Deleting a Row-level access policy**

This can be done using the following commands:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693317649075/dd53bf17-c542-431a-961b-1ed131f6f62e.png align="center")

Thanks for reading!

---

🚀 Delving into BigQuery, Google Cloud and Analytics? Stay connected with me for valuable insights, handy tips, and strategies to effortlessly traverse the vast universe of cloud computing and data analytics!

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*