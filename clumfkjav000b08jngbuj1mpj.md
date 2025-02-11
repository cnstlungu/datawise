---
title: "A portable Data Analytics stack using Docker, Mage, dbt-core, DuckDB and Superset"
datePublished: Fri Apr 05 2024 08:55:24 GMT+0000 (Coordinated Universal Time)
cuid: clumfkjav000b08jngbuj1mpj
slug: a-portable-data-analytics-stack-using-docker-mage-dbt-core-duckdb-and-superset
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/tjX_sniNzgQ/upload/f62cd5d28270ba6459c3b3d60b6a0834.jpeg
tags: analytics, docker, dbt, duckdb, apache-superset, mageai

---

Just wanted to share a [small learning-by-doing project of mine](https://github.com/cnstlungu/portable-data-stack-mage). It's a containerized Data Analytics suite, covering end-to-end analytics process for a small (imaginary) company.

We're talking about:  
\- generating example data in parquet files using Python  
\- ingesting data into DuckDB  
\- model data using dbt-core  
\- loading a DuckDB datamart  
\- orchestrate using MageAI  
\- displaying it all in a Superset dashboard.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712307192300/d55dacd3-e001-4537-816d-2eaf36e94d23.png align="center")

Each of the components is in a separate Docker container, tied all together with docker-compose.

I've previously set up similar projects with [Airflow](https://github.com/cnstlungu/portable-data-stack-airflow) and [Dagster](https://github.com/cnstlungu/portable-data-stack-dagster).

It's pretty bare bones (somewhat as intended) and has some rough edges, but it should be a good starting point for a demo, template or learn how all these components works together.

I would of course appreciate any feedback or suggestions on how to make it better.

*Found it useful? Check out to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*