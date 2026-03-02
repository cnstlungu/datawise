---
title: "A quick overview of BigQuery functions"
seoTitle: "BigQuery Functions: A Quick Overview"
seoDescription: "Explore BigQuery functions: built-in, custom, and remote. Learn about their types, uses, and how they enhance SQL capabilities"
datePublished: Sun Mar 02 2025 20:57:27 GMT+0000 (Coordinated Universal Time)
cuid: cm7s4427e00000ala3kgtdh8f
slug: a-quick-overview-of-bigquery-functions
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/cHhbULJbPwM/upload/aff47b5d4d7d6ac7457150c035267f20.jpeg

---

When we talk about functions in **BigQuery**, we're referring to several distinct capabilities.

Beyond the standard built-in functions like CURRENT\_TIMESTAMP() or LENGTH(), BigQuery helps users to define custom functions that extend SQL capabilities. These user-defined functions belong to the larger category of routines (alongside stored procedures), enabling logic reuse.

🔹 Types of Functions in BigQuery

By Duration

➡️ Persistent functions – Stored in your dataset and reusable across all sessions

➡️ Temporary functions – Available only within your current session (created with TEMP keyword)

By Return Type

➡️ Scalar functions – Return a single value per input row (which can be complex types like structs or arrays) → typically used in SELECT or WHERE clauses

➡️ Table-Valued Functions (TVFs) – Return entire tables, requiring you to SELECT FROM the function

BigQuery functions can be written in either SQL or JavaScript.

Based on their processing nature:

➡️ Regular UDFs – Process individual rows, transforming inputs into a single output value

➡️ User-Defined Aggregate Functions (UDAFs) – Combine multiple rows into a single result using custom logic (currently in preview)

🔹 Beyond BigQuery: Remote Functions

For complex processing requirements, BigQuery offers remote functions, which allows us to:

➡️ Send data to Google Cloud Functions or other external services

➡️ Process it using a programming language

➡️ Return results to our query

This opens access to the vast ecosystem of libraries in languages like Python.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1740949017916/8a2445da-f34f-4a89-8dbc-966270b5d657.png align="center")

### Their Place in Modern **SQL**

Back in the day when I just started with **SQL Server**, I used scalar functions sparingly (as a junior I was always warned about performance 🤓) and occasionally employed TVFs for small reusable datasets.

Today, with modern transformation frameworks like dbt and Dataform, I find myself almost not using BigQuery — the same reusable logic is now defined as macros or custom JS functions within these frameworks.

💡 I'm curious:

➡️ How often do you use UDFs or TVFs in your SQL environment?

➡️ Do you prefer handling reusable logic in your SQL code or in external frameworks?

➡️ Any interesting use cases you've seen for remote functions for unusual/specialized processing needs?

*Found it useful? Subscribe to my Analytics newsletter at* [***notjustsql.com***](https://notjustsql.com/)*.*