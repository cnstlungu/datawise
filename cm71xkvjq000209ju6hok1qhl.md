---
title: "Choosing the Right Ranking Function: Why Ties in SQL Matter"
datePublished: Wed Feb 12 2025 13:12:33 GMT+0000 (Coordinated Universal Time)
cuid: cm71xkvjq000209ju6hok1qhl
slug: choosing-the-right-ranking-function-why-ties-in-sql-matter
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/M8QfxX2EQXo/upload/274d14c532af72317f6e687291b841f7.jpeg
tags: databases, google-cloud, sql, bigquery, data-engineering

---

If you’re like me, you probably use QUALIFY + ROW\_NUMBER() almost daily for deduplication or finding the first/last occurrence of something. It’s a powerful combo in modern SQL !  
  
But here’s the catch: there are subtle nuances and edge cases that can cause some trouble.  
  
The choice between ordering functions like ROW\_NUMBER(), DENSE\_RANK(), and RANK() isn’t always straightforward—it depends on the nature of your data and the question you’re trying to answer.

Check out [my previous post](https://datawise.dev/comparing-ranking-functions-in-bigquery) a quick overview of ordering functions.  
  
Now, let me share a scenario.  
  
We want to find the first event type for each user. Simple enough, right?  
But in this case we can have two events happening at the exact same time.  
  
Here’s where things get interesting:  
➡️ ROW\_NUMBER() would arbitrarily pick one event and mask the tie (non-deterministic behavior).  
➡️ DENSE\_RANK(), on the other hand, would preserve the tie, allowing us to decide how to handle it.  
  
This subtle difference can have a huge impact on your results!  
  
TL;DR: Keep ties in mind when deciding which numbering function to use.  
  
As always, it’s about using the right tool for the right job.  
  
Have you encountered any tricky scenarios with ties?

*Found it useful? Subscribe to my Analytics newsletter at* [***notjustsql.com***](http://notjustsql.com/)*.*