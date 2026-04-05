---
title: "Parameters in BigQuery"
seoTitle: "BigQuery Parameters vs Variables: What's the Difference?"
seoDescription: "Parameters and variables both hold typed values in BigQuery, but they solve different problems. Learn when to use query parameters for user input and when variables fit scripting workflows."
datePublished: Sat Feb 07 2026 12:37:25 GMT+0000 (Coordinated Universal Time)
cuid: cmlcaud04000802jv5gzp5qxk
slug: parameters-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/vzbXoo0CuAs/upload/1df97efa0e7dba248f0b2e697e4fe6bf.jpeg

---

You can use query parameters in BigQuery hashtag#SQL (now in the console as well!) — but how are they different from variables, and when should you use each?

Both parameters and variables act as placeholders and have a defined data type. The difference is where their value comes from and how they’re used.

Parameters (like @corpus)  
👉 Are not computed inside the query  
👉 Are passed from the outside (Python, UI, API, etc.)

Variables (DECLARE, SET)  
👉 Are defined and computed inside a SQL script or stored procedure  
👉 Let you store a value and reuse it later in the same script

So what’s the real difference?  
➡️ Variables are essential for Dynamic SQL (EXECUTE IMMEDIATE)  
➡️ Parameters can filter data, but cannot control identifiers (e.g. table or column names)

🚨 Security  
When values come from user input or external sources, parameters are the safer choice—they reduce the risk of SQL injection.

🚅 Performance  
Parameters may allow the optimizer to reuse execution plans, while variables can sometimes prevent that.

![](https://cdn.hashnode.com/uploads/covers/641c1535429c76261884ecba/587b5764-27e3-4ae9-b1b9-7d9491d2663e.png align="center")

*Found it useful? Check out to my Analytics newsletter at* [*notjustsql.com*](https://notjustsql.com)*.*