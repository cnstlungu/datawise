---
title: "Leveraging ARRAYS in BigQuery for query performance"
datePublished: Tue Dec 19 2023 22:46:25 GMT+0000 (Coordinated Universal Time)
cuid: clqcxp87e000108jrejscce9g
slug: leveraging-arrays-in-bigquery-for-query-performance
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/VhDgReMsz8w/upload/de24b096bb46c8b5384f6a4c7dd33b98.jpeg
tags: analytics, google-cloud, sql, bigquery, data-engineering

---

Leveraging your platform functionality goes a long way. When developing data pipelines, besides the functional requirements, we try to optimize for some other important variables, such as cost, resources consumed or runtime. While working with big or complex datasets in BigQuery, I always try a test several approaches to see which one yields a better mix from the above.

Take ARRAYs, for example. They allow us to define one-to-many relationships inside tables while saving up on storage and potentially processing power too.

I'll provide a short example. Say we have 100 customers and several thousand dates they visited a website. We could store this in two ways:

\- classic approach with one row representing a unique id-date combination  
100 ids x 3640 dates each = 364k rows

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703025880184/f4a08d51-c96f-482a-aebf-a1cb9023a1fa.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703025895764/86105b9a-8517-488e-af76-9f96faee4322.png align="center")

\- leveraging ARRAYs and having one row = one id and its array of dates.  
100 ids with an array of 3640 dates each = 100 rows

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703025825407/fcd1aecd-d969-44d7-ad24-4e2fe60c435b.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1703025860461/a2241a57-2a07-4326-86bc-6dc2442d5a78.png align="center")

Let's run a quick query to test the performance of these two. In this particular case, the array example consumes a minuscule fraction of the slot time of the non-array example while still processing only half as many bytes.

![](https://miro.medium.com/v2/resize:fit:1400/0*QEMcxStBEVdtgtmc align="left")

I'm definitely not saying this is a "one size fits all" approach, depending of course on data structure, size, querying patterns and other constraints. But whenever you have a challenge like that, it's good to know your options, try out different strategies and pick the one that suits your use case best.

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*