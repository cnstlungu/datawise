---
title: "LIKE ALL and LIKE ANY in BigQuery"
datePublished: Tue Dec 05 2023 23:01:17 GMT+0000 (Coordinated Universal Time)
cuid: clpsy2f8o000108l243wxftf3
slug: like-all-and-like-any-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/7JX0-bfiuxQ/upload/dbecb45935a86d433879fee746f0f908.jpeg
tags: analytics, databases, google-cloud, sql, bigquery, data-engineering

---

Let's look at the quantified LIKE operator in BigQuery. Why quantified? , you'll ask.

So while the normal LIKE operator can be used to check just for one pattern, the quantified one (still in preview btw) can check the presence of one or all patterns from a sequence we provide. Here's how the syntax looks.

`WHERE text LIKE ALL ('%dog%', '%fox%')` - this will check if ALL the patterns are present in the text

```sql
WITH input_data AS 

(
  SELECT 'The quick brown fox jumps over the lazy dog' AS text
  UNION ALL
  SELECT 'My favorite dog is a Labrador' AS text
)

SELECT text FROM input_data

WHERE text LIKE ALL ('%dog%', '%fox%')

-- returns only the first row, since only that one has both dog and fox
```

`WHERE text LIKE SOME ('%dog%', '%fox%')` and  
`WHERE text LIKE ANY ('%dog%', '%fox%')` - these two are synonyms and will check if AT LEAST ONE of the listed patterns is present in the text

```sql
WITH input_data AS 

(
  SELECT 'The quick brown fox jumps over the lazy dog' AS text
  UNION ALL
  SELECT 'My favorite dog is a Labrador' AS text
)

SELECT text FROM input_data

WHERE text LIKE ALL ('%dog%', '%fox%')
-- returns both rows, since both match at least one pattern
```

Pair them with the NOT keyword to achieve the opposite effect, so NOT LIKE ANY/SOME means not even a partial match and NOT LIKE ALL means no full match.

Thanks for reading!

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*