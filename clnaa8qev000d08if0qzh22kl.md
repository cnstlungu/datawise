---
title: "Write better SQL queries faster using Mock Data"
datePublished: Tue Oct 03 2023 12:15:05 GMT+0000 (Coordinated Universal Time)
cuid: clnaa8qev000d08if0qzh22kl
slug: write-better-sql-queries-faster-using-mock-data
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/uGbG4LnMFMY/upload/5a85ec57b603763fe442ed7b9e1f7fa9.jpeg
tags: analytics, databases, sql, bigquery

---

🛠️ Here's a technique I frequently employ to streamline my query development process.

Ever find yourself stuck in the complexity of writing non-trivial queries, especially with voluminous tables? 🤔 The amalgamation of query complexity and business problems can sometimes make writing your [#SQL](https://www.linkedin.com/feed/hashtag/?keywords=sql&highlightedUpdateUrns=urn%3Ali%3Aactivity%3A7114896527554195458) take more time than necessary.

When exploring a new coding approach, utilizing an unfamiliar function, or navigating through unseen data, I create a simplified, representative example using dummy data and a few test cases.

In a blank [#BigQuery](https://www.linkedin.com/feed/hashtag/?keywords=bigquery&highlightedUpdateUrns=urn%3Ali%3Aactivity%3A7114896527554195458) window, I write a couple of Common Table Expressions (CTEs) to simulate input, then focus on mimicking only the pivotal columns - maintaining the grain and incorporating one representative value, along with the join columns. A single value can often represent a surrogate key for the grain of the tables.

🚀 This approach enables me to:

\- Iterate rapidly, considering edge cases irrespective of the data subset.  
\- Sharpen the technical requirements by applying the solution to the available data and addressing the business question.  
\- Contemplate how the technical solution can be optimized for data scale and manage real-world corner cases or unexpected scenarios.  
\- Save processing costs, since I'm working only on kilobytes of data until I have a solution that is &gt;80% ready

👀 So, the next time you have to write a big query (pun unintended), especially when dealing with unfamiliar data or functions, take a moment to code a swift example in a blank BigQuery window. It pays off to think simply first.

🔄 Is this Test-Driven Development (TDD) for BigQuery? Perhaps. I like to term it *Iterative Development*.

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*