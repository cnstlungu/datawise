---
title: "Filling in missing data in BigQuery"
seoTitle: "Practical Guide to Filling in Missing Data in BigQuery"
seoDescription: "Learn how to fill in missing data in BigQuery using practical methods such as LAG, UNPIVOT, and PIVOT, including code examples and step-by-step explanations"
datePublished: Mon Feb 27 2023 11:56:27 GMT+0000 (Coordinated Universal Time)
cuid: clfn1r5ys000b09l967kobbpe
slug: practical-bigquery-filling-in-missing-data
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/5B0IXL2wAQ0/upload/f5a7782fd7048c55a1967623a5af29d7.jpeg
tags: analytics, sql, bigquery, gcp, datawarehouse

---

Data comes in a vast range of shapes and sizes for Data Engineers, with common categories being structured data (such as a database table), semi-structured (such as JSON or XML), and unstructured data (such as text or images). Naturally, the requirements for the result can be quite varied as well. In this article, we’ll explore some typical obstacles that Data Engineers face when integrating data through a case study, to meet a specific requirement based on a given input.

### The input

In this particular case, the data is arriving at a BigQuery from a source system, albeit in a very particular fashion. Each event can be either a full event (with all the *attributes* ) or can have only one (or more) event attribute, with the other attributes being NULL.

%[https://gist.github.com/cnstlungu/5d1e47ae3b024fad0b31a0c8b7e68d45] 

### The desired outcome

From the input above, we’d like to obtain a structure that will allow us to tell, at any point in time, what is the state of all attributes (or their last known state at the moment), akin to a temporal fact table.

%[https://gist.github.com/cnstlungu/462119264ef8a8e3c14cac98787dcc24] 

### Analyzing our options

Typically when we’d like to access a previous value, we could use the LAG function with a window expression, as below:

```sql
SELECT input_data.country_id, input_data.store_id, input_data.event_time, input_data.attribute1,

LAG(input_data.attribute1) OVER(PARTITION BY country_id, store_id ORDER BY input_data.event_time) AS previous_value

FROM input_data

WHERE store_id = 'DE1004'

ORDER BY event_time DESC
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563509045/89857191-0170-45cd-98dc-a38eadc6583f.png align="left")

Now, there is a couple of problems with the above approach.

First, the LAG function in BigQuery does not support a ‘IGNORE NULLS’ command at the moment, so we end up getting the previous value (even if it is a NULL) when we’re interested in the most recent non-NULL value.

Second, we’d need to apply such a transformation to each attribute. We might get away with 10 attributes, but how about when we have several dozens of them?

### Let’s (un)pivot

It would be great if we can transpose all these attributes from columns to rows. For this, we have the UNPIVOT function. We’d first need to cast the attributes to a common data type (typically STRING) — that is because all the same inside the new column must have the same data type.

Then we can UNPIVOT the value of each attribute, thus obtaining two columns: the attribute and its value.

```sql
WITH processed AS (

SELECT

event_time,
country_id,
store_id,
attribute1,
CAST(attribute2 AS STRING) AS attribute2,

FROM input_data

)

SELECT

event_time,
country_id,
store_id,
attribute,
value

FROM processed
UNPIVOT(value FOR attribute IN (attribute1, attribute2))
```

%[https://gist.github.com/cnstlungu/94e4cafb1c8829155890038ceb8b5cc8] 

But there is a problem with this approach. As you can see above, we’re getting a dense table — so there are no NULL entries for our attributes. That is because UNPIVOT ignores NULL values. We need something else to help us get the sparse table, a way to unpivot the values while keeping the nulls.

And then I found an interesting approach in a [Stack Overflow answer](https://stackoverflow.com/questions/64948819/split-key-value-pairs-to-columns-in-google-bigquery).

I’ve adapted it for our needs, namely to work around the fact that an attribute could be a timestamp, which contains a colon. So what does the below code do?

* We start by converting the row into a JSON object
    
* We’re splitting it into key-value pairs
    
* Using regular expressions, we extract the part before the first colon — the key (attribute)
    
* We also extract the part after the first colon — the value
    
* Since JSON is going to provide a ‘null’ string, we’re converting that to an actual NULL
    

```sql
WITH processed AS (

SELECT

event_time,
country_id,
store_id,
attribute1,
CAST(attribute2 AS STRING) AS attribute2,

FROM input_data

)

SELECT

event_time,
country_id,
store_id,
REGEXP_EXTRACT(kvp, '([^:]+)') AS attribute,
NULLIF(REGEXP_EXTRACT(kvp, ':(.*)' ), 'null') AS value

FROM processed i,

UNNEST(SPLIT(REGEXP_REPLACE(TO_JSON_STRING(i), r'[{}"]', ''))) kvp
```

This yields the following results:

%[https://gist.github.com/cnstlungu/c3b6a60c3f6deb4bf6ee92e1e1521a5e] 

You can now notice we have our sparse table, including the null (represented above as missing) attribute values.

Now, it’s time for us to fill in the gaps for each attribute value with the last non-NULL value. We’ve already mentioned that the LAG window function ignores NULLs, so we need another way to achieve this. Once again, it’s [StackOverflow to the rescue](https://stackoverflow.com/questions/65506809/bigquery-lag-navigation-function-ignore-nulls).

In this code, we’re:

* defining a window over our non-changing columns (*country\_id*, *store\_id*) + *attribute*, ordering it by *event\_time* decreasingly
    
* leveraging the NTH\_VALUE column with IGNORE NULLS
    
* If there is a value, we keep it, otherwise extract the last non-NULL event in our window
    

```sql
SELECT

event_time,
country_id,
store_id,
attribute,
value AS actual_value,
COALESCE(value, NTH_VALUE(IFNULL(value, NULL), 1 IGNORE NULLS) OVER previous_events) AS computed_value

FROM unpivoted

WINDOW previous_events AS (
PARTITION BY country_id, store_id, attribute ORDER BY event_time DESC ROWS BETWEEN 1 FOLLOWING AND UNBOUNDED FOLLOWING)
```

This yields the following result:

%[https://gist.github.com/cnstlungu/f8008f0cd3dab3c74973dc932cf401fd] 

### Pivoting the data

We can now PIVOT the data back to its original form. We’d need an aggregate function like ANY\_VALUE as well as CAST to the attribute value’s original datatype. Given we’re using an aggregate function, we’d also need to use GROUP BY.

```sql
SELECT

event_time,
country_id,
store_id,
ANY_VALUE(attribute1) AS attribute1,
CAST(ANY_VALUE(attribute2) AS int64) AS attribute2,
CAST(ANY_VALUE(attribute3) AS int64) AS attribute3,
CAST(ANY_VALUE(attribute4) AS bool) AS attribute4,
ANY_VALUE(attribute5) AS attribute5,
CAST(ANY_VALUE(attribute6) AS int64) AS attribute6,
CAST(ANY_VALUE(attribute7) AS int64) AS attribute7,
CAST(ANY_VALUE(attribute8) AS bool) AS attribute8,
ANY_VALUE(attribute9) AS attribute9,
CAST(ANY_VALUE(attribute10) AS int64) AS attribute10

FROM computed_values

PIVOT(ANY_VALUE(computed_value) FOR attribute IN

('attribute1','attribute2', 'attribute3', 'attribute4', 'attribute5', 'attribute6', 'attribute7', 'attribute8', 'attribute9', 'attribute10'))

GROUP BY event_time, country_id, store_id
```

%[https://gist.github.com/cnstlungu/77e8090909531487b6fb74d6e689ed34] 

### Final touches

With data now pivoted, we can create the temporal structure. We’re going to:

* Consider the *event\_time* as *valid\_from*
    
* Use the LEAD window function to retrieve the next event
    
* Subtract a second from the next event and consider that as *valid\_to*
    
* In case there is no future event (this being a current\_state), provide a placeholder with a date well into the future i.e. ‘2999–12–31 23:59:59 UTC’
    

```sql
SELECT
    
    country_id,
    store_id
    event_time AS valid_from,
    IFNULL(DATE_SUB(LEAD(event_time,1) OVER(PARTITION BY country_id, store_id ORDER BY event_time ASC ), INTERVAL 1 SECOND), '2999-12-31 23:59:59 UTC') AS valid_to,
    attribute1,
    attribute2,
    attribute3,
    attribute4,
    attribute5,
    attribute6,
    attribute7,
    attribute8,
    attribute9,
    attribute10

FROM pivoted
```

We can now query the history of changes to see its state at any point in time, including the current state.

```sql
SELECT
    
    country_id,
    store_id,
    valid_from,
    valid_to,
    attribute1,
    attribute2,
    attribute3,
    attribute4,
    attribute5,
    attribute6,
    attribute7,
    attribute8,
    attribute9,
    attribute10
    
FROM final_table

WHERE CURRENT_TIMESTAMP() BETWEEN valid_from and valid_to
```

%[https://gist.github.com/cnstlungu/462119264ef8a8e3c14cac98787dcc24] 

### Conclusion

In this practical exercise, we’ve looked at transforming variable-schema event data in BigQuery into a temporal structure, allowing us to query the state of all the attributes at any point in time.

Thanks for reading and stay tuned for other interesting posts about Data Engineering.

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*