---
title: "Revisiting GROUP BY ROLLUP with a more realistic example"
datePublished: Sat Feb 22 2025 14:56:13 GMT+0000 (Coordinated Universal Time)
cuid: cm7gbooyb000c09lagnce7532
slug: revisiting-group-by-rollup-with-a-more-realistic-example
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/PB80D_B4g7c/upload/3acf41a5d990604edcf90a65ed72979e.jpeg
tags: analytics, databases, google-cloud, sql, bigquery, data-engineering

---

Ever had a random piece of knowledge from school suddenly click in a real-world scenario?

It felt like that for me remembering about ROLLUP a few days ago.

I wrote about GROUP BY ROLLUP roughly 1.5 years ago—[one of my first posts here](https://datawise.dev/using-rollup-in-bigquery). At the time, it was unfamiliar to me, and I had no idea I’d ever need it. But this week, I finally encountered a real use case.

𝐓𝐡𝐞 𝐏𝐫𝐨𝐛𝐥𝐞𝐦

Imagine we have sales data for a retail store, where each product belongs to a subcategory and a category (e.g., Apples → Fruits → Food).

We want to compute the average ordered quantity per product, but with a hierarchical fallback:  
1. If there’s no product-level data, use the subcategory average.  
2. If that’s missing, use the category average.  
3. If still unavailable, fall back to the overall average across all products.

𝐇𝐨𝐰 𝐑𝐎𝐋𝐋𝐔𝐏 𝐇𝐞𝐥𝐩𝐬

When we GROUP BY ROLLUP (category, subcategory, product\_id), we get multiple aggregation levels in one query:  
✅ Per product  
✅ Per subcategory  
✅ Per category  
✅ Across all rows

This allows us to build a lookup table, which we can use with multiple LEFT JOINs to apply the fallback logic.

𝐋𝐞𝐭'𝐬 𝐭𝐞𝐬𝐭 𝐢𝐭

Here’s how it works in practice:  
• Apples → Direct sales data → AVG(quantity) = 6  
• Mangoes → No past sales → Uses Fruits subcategory → AVG(quantity) = 4.67  
• Cucumbers → No past sales, no Vegetables subcategory data → Uses Food category → AVG(quantity) = 4.67  
• Washing Machine → No sales data, no relevant category → Uses overall average → AVG(quantity) = 6

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1740236002221/32bcd67e-bad3-4d76-845a-1b5602877a50.jpeg align="center")

𝐈𝐧 𝐥𝐢𝐞𝐮 𝐨𝐟 𝐚 𝐜𝐨𝐧𝐜𝐥𝐮𝐬𝐢𝐨𝐧

This was a fun experiment, but let’s be honest—this could also be done with window functions!

Still, ROLLUP provides an perspective, and I’m on the lookout for an even better use case.

Have you ever had an SQL feature suddenly “click” for you?

*Found it useful? Subscribe to my Analytics newsletter at* [***notjustsql.com***](https://notjustsql.com/)*.*