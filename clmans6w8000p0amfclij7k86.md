---
title: "Using MAX_BY / MIN_BY in BigQuery"
datePublished: Fri Sep 08 2023 13:54:25 GMT+0000 (Coordinated Universal Time)
cuid: clmans6w8000p0amfclij7k86
slug: using-maxby-minby-in-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/iLKK0eFTywU/upload/8b848b1e33dbc6099a5bda081ea8066d.jpeg
tags: google-cloud, sql, bigquery

---

Just stumbled upon a nifty SQL function in BigQuery that was new to me.

Did you know about `MAX_BY / MIN_BY`? They're essentially shortcuts for `ANY_VALUE(columnA HAVING MIN/MAX(columnB))`. And guess what? I had no idea you could use `HAVING` within `ANY_VALUE`.

So, what does it do? It fetches the value from one column based on the minimum or maximum value of another column.

Here's a quick example of how it works.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694181196618/16a4a82e-d6f4-4a01-b3ad-8cfdfc921b18.png align="center")

```sql
WITH employees AS (

  SELECT 'Jane' AS first_name, 'Doe' AS last_name, 75000 AS gross_salary, '2020-01-01' AS hire_date

  UNION ALL

  SELECT 'Callum' AS first_name, 'Blake' AS last_name, 55000 AS gross_salary, '2022-06-01' AS hire_date

  UNION ALL

  SELECT 'Jack' AS first_name, 'Dew' AS last_name, 77000 AS gross_salary, '2019-03-01' AS hire_date

  UNION ALL

  SELECT 'Emily' AS first_name, 'Scott' AS last_name, 80000 AS gross_salary, '2021-01-01' AS hire_date

)

SELECT 

MAX_BY(CONCAT(first_name,' ', last_name), gross_salary) AS employee_with_highest_gross_salary,
--same as 
ANY_VALUE(CONCAT(first_name,' ', last_name) HAVING MAX(gross_salary)) AS also_employee_with_highest_gross_salary,


MIN_BY(CONCAT(first_name,' ', last_name), hire_date) AS employee_hired_earliest,
--same as
ANY_VALUE(CONCAT(first_name,' ', last_name) HAVING MIN(hire_date)) AS also_employee_hired_earliest

FROM employees
```

This would produce the following output:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694181225127/6677da6c-44d8-4ecd-9c8c-eed2dfeef495.png align="center")

In our field, every day is a learning journey. Stay tuned for more insights on Analytics, SQL, Python and BigQuery. Follow along!

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*