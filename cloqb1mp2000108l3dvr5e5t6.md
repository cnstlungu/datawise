---
title: "Tidying up WINDOW functions in BigQuery with named windows"
datePublished: Wed Nov 08 2023 22:01:34 GMT+0000 (Coordinated Universal Time)
cuid: cloqb1mp2000108l3dvr5e5t6
slug: tidying-up-window-functions-in-bigquery-with-named-windows
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/Q0aQcZV0oug/upload/347852134efe5bcd4d475525203f5279.jpeg
tags: analytics, databases, sql, bigquery

---

So, if you ever find yourself working with multiple window functions in BigQuery, leverage the named windows specification for tidier, leaner code.

Say you have a function like:

`DENSE_RANK() OVER (PARTITION BY country ORDER BY hire_date)`.

You can extract the `(PARTITION ... ORDER...)` part to a named window and then reuse this partitioning window for other calculations, thus having to write less code.

Let's look at a practical example of how it's done.

Here's our input data:

```sql
+-------------+------------+-----------+--------------+------------+--------------------+----------+---------+
| employee_id | first_name | last_name | gross_salary | hire_date  | position           | store_id | country |
+-------------+------------+-----------+--------------+------------+--------------------+----------+---------+
| F2          | Jane       | Doe       | 75000        | 2020-01-01 | Senior Salesperson | F100     | France  |
| F4          | Callum     | Blake     | 55000        | 2023-06-01 | Junior Salesperson | F100     | France  |
| F1          | Jack       | Dew       | 77000        | 2019-03-01 | Salesperson        | F200     | France  |
| F3          | Emily      | Scott     | 80000        | 2021-01-01 | Salesperson        | F200     | France  |
| G4          | Josh       | Woods     | 85000        | 2020-01-01 | Senior Salesperson | G100     | Germany |
| G5          | Callum     | Blake     | 65000        | 2022-09-01 | Salesperson        | G100     | Germany |
| G2          | Johann     | Frost     | 87000        | 2017-06-01 | Senior Salesperson | G200     | Germany |
| G3          | Francis    | Drake     | 80000        | 2018-04-01 | Senior Salesperson | G200     | Germany |
| G1          | Germain    | Muller    | 90000        | 2017-04-01 | Senior Salesperson | G200     | Germany |
+-------------+------------+-----------+--------------+------------+--------------------+----------+---------+
```

Now, there's a series of metrics we'd need to compute for comparison with each employee. We'd ideally need WINDOW functions for these:

* an average gross salary per store
    
* a count of employees per store
    
* a maximum gross salary paid for the same position in the respective country
    
* an ordering of employees in each country based on hire date
    

Instead of writing multiple time something like `OVER (PARTITION BY store_id)` , we can give this partitioning window a name - in this case store\_window and define it in the WINDOW specification, as shown below.

Note that calculations that use the same window definition can re-use the same named window.

```sql
SELECT
first_name, last_name, gross_salary, hire_date, position, store_id, country,
AVG(gross_salary) OVER store_window AS avg_salary_per_store,
COUNT(DISTINCT employee_id) OVER store_window AS no_employees_in_store,
MAX(gross_salary) OVER country_position_window AS max_salary_country_same_position,
DENSE_RANK() OVER country_tenure_window AS order_of_employement_country

FROM employees

WINDOW store_window AS (PARTITION BY store_id), 
       country_store_window AS (PARTITION BY country, store_id), 
       country_position_window AS (PARTITION BY country, position),
       country_tenure_window AS (PARTITION BY country ORDER BY hire_date)
```

See below the output of this query.

```sql
+------------+-----------+--------------+------------+--------------------+----------+---------+----------------------+-----------------------+----------------------------------+-----------------------------+
| first_name | last_name | gross_salary | hire_date  | position           | store_id | country | avg_salary_per_store | no_employees_in_store | max_salary_country_same_position | order_of_employment_country |
+------------+-----------+--------------+------------+--------------------+----------+---------+----------------------+-----------------------+----------------------------------+-----------------------------+
| Jack       | Dew       | 77000        | 2019-03-01 | Salesperson        | F200     | France  | 78500.0              | 2                     | 80000                            | 1                           |
| Jane       | Doe       | 75000        | 2020-01-01 | Senior Salesperson | F100     | France  | 65000.0              | 2                     | 75000                            | 2                           |
| Emily      | Scott     | 80000        | 2021-01-01 | Salesperson        | F200     | France  | 78500.0              | 2                     | 80000                            | 3                           |
| Callum     | Blake     | 55000        | 2023-06-01 | Junior Salesperson | F100     | France  | 65000.0              | 2                     | 55000                            | 4                           |
| Germain    | Muller    | 90000        | 2017-04-01 | Senior Salesperson | G200     | Germany | 85666.666666666672   | 3                     | 90000                            | 1                           |
| Johann     | Frost     | 87000        | 2017-06-01 | Senior Salesperson | G200     | Germany | 85666.666666666672   | 3                     | 90000                            | 2                           |
| Francis    | Drake     | 80000        | 2018-04-01 | Senior Salesperson | G200     | Germany | 85666.666666666672   | 3                     | 90000                            | 3                           |
| Josh       | Woods     | 85000        | 2020-01-01 | Senior Salesperson | G100     | Germany | 75000.0              | 2                     | 90000                            | 4                           |
| Callum     | Blake     | 65000        | 2022-09-01 | Salesperson        | G100     | Germany | 75000.0              | 2                     | 65000                            | 5                           |
+------------+-----------+--------------+------------+--------------------+----------+---------+----------------------+-----------------------+----------------------------------+-----------------------------+
```

As you've seen from the above, the named WINDOW approach is pretty handy and clean, as opposed to individually specifying the window in the function call.

Thanks for reading!

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*