---
title: "Null-safe comparison: IS DISTINCT/NOT DISTINCT FROM"
seoTitle: "Understanding NULL-safe comparisons"
seoDescription: "Discover NULL-safe SQL operators IS DISTINCT FROM and IS NOT DISTINCT FROM for safer comparisons without IFNULLs or COALESCE in BigQuery"
datePublished: Tue May 06 2025 07:32:11 GMT+0000 (Coordinated Universal Time)
cuid: cmac6yv68000d09hza6gm41ob
slug: null-safe-comparison-is-distinctnot-distinct-from
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/MJAoiige14E/upload/55425a149a5b1659f0fd86d54b53737e.jpeg
tags: analytics, google-cloud, sql, bigquery, data-engineering

---

I've been working for surprisingly long with SQL to have found this only a few days ago. Not long enough I guess 🤓.

I'm talking about the NULL-safe operators IS DISTINCT FROM and IS NOT DISTINCT FROM. I found about their existence from a [Linkedin post](https://www.linkedin.com/posts/sebastian-flak_the-sql-comparison-operator-you-should-activity-7322288997945212928-3hOZ?utm_source=share&utm_medium=member_desktop&rcm=ACoAAAvrnvABKPsQ1CE0m9jhBpQ-Vr-YZbN9dqg).

Works on BigQuery too, so I guess less need of adding IFNULLs / COALESCE for safety.

![](https://miro.medium.com/v2/resize:fit:700/0*Wb4zGkbHhG9oEoVC align="left")

PS This choice of keyword "FROM", together with the one in EXTRACT(HOUR FROM DATETIME '2021-01-01'), feels pretty weird.

*Found it useful? Subscribe to my Analytics newsletter at* [***notjustsql.com***](https://notjustsql.com/)*.*