---
title: "9 tips on writing cleaner SQL"
seoTitle: "9 tips on writing better SQL"
seoDescription: "This article provides nine tips for writing cleaner SQL queries. The tips include formatting queries, using meaningful aliases, avoiding SELECT *, using com"
datePublished: Sun Sep 25 2022 21:43:23 GMT+0000 (Coordinated Universal Time)
cuid: clfl7llh4000009kzc39o7zvn
slug: 9-tips-on-writing-cleaner-sql
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1679582456366/1c751524-8bae-410a-a1ea-d58f7cac96cd.jpeg
tags: analytics, sql, bigquery, gcp, data-engineering

---

Structured Query Language, widely recognized by its acronym SQL (whether you pronounce it as es-queue-el or sequel), is one of the most widely used languages to retrieve and process data. While it’s been around for already half a century, there’s no indication that it might go away soon. Millions of DBAs, developers, data analysts and data engineers write SQL commands daily.

In this short article, we’re going to look at a couple of tips on how to improve our SQL queries and make them more readable, clean and maintainable.

### Format your queries

The first thing we need to look at is how we format the queries. There are many ways how to go about this, but the below should be a good start. Remember a lot of time would be spent reading SQL (written by yourself or by someone else), so a little effort in arranging the code would pay off in the long term.

#### Capitalize SQL keywords

SQL doesn’t enforce a case for the keywords, but it might the core will be more readable if you capitalize SQL keywords to visually distinguish them from the column and table names.

%[https://gist.github.com/cnstlungu/9012e16d52ebb7ba1e9feccfe9be893a] 

#### Use consistent indentation

It is good to pick an indentation pattern and be consistent. I’d suggest using tabs instead of spaces for indentation.

%[https://gist.github.com/cnstlungu/eb6d68314f7a799fd781933a991c83ca] 

#### Aliasing

Avoid implicit column aliasing as it is a source of confusion.

%[https://gist.github.com/cnstlungu/ee27a42e65a49bcf2efdaa9a67771a7e] 

Give concise yet meaningful aliased to columns, CTEs, subqueries and tables while adhering to consistent naming conventions

%[https://gist.github.com/cnstlungu/cf3b0b822c10b461b0e5c8d596494e65] 

If selecting data from multiple tables, use the table name or table alias in the select list to identify which column comes from which table.

%[https://gist.github.com/cnstlungu/ff8408fdaa5e6812233fa184fad1916b] 

#### Avoid SELECT \*

SELECTING \* might seem handy, but it opens the door for a whole lot of maintenance headaches and performance issues. It is preferable to explicitly name the columns you’d like to select.

%[https://gist.github.com/cnstlungu/ae94a5f7a6ab882967ddc3268a61e917] 

### Comments

Comments can be very helpful when maintaining code that somebody else wrote, potentially in absence of other documentation. It could also help identify bugs when the stated intent does not coincide with what the code does (or does not anymore). Of course, a middle ground needs to be found between putting too much information and providing not enough context.

* Use multi-line comments for explaining the desired intent of a particular script, for detailed explanations or instructions.
    
* Use single-line comments to annotate your code to make servicing easier.
    

%[https://gist.github.com/cnstlungu/64c207857e33407022b7e2a59e98b402] 

### Avoid nested queries and use CTEs

While a nested query and a Common Table Expression (CTE) should (at least in theory) have equivalent performance, the CTE is much more readable and handier when debugging.

%[https://gist.github.com/cnstlungu/95fea3e49a750d863039e9d6e52f0d2d] 

This becomes more obvious as the query complexity grows.

%[https://gist.github.com/cnstlungu/246fb0f68ba8f8b75967328beab47d45] 

### Work only with data that you need

When working with complex queries that include CTEs or subqueries, it helps if we query only the columns and rows that are used one way or another down the line.

Therefore, filter out as much data as you can, as early as you can. Bring it to the smallest amount of columns and rows you’d need to solve the problem. **Again, keep only the columns and the rows you need**.

### If something is tedious, there’s probably a way to do it smarter

For instance, in SQL Server, when trying to pivot a result set, you need to provide the new column names. If you have a dozen of columns, or if these things change, this might be a tedious task. A quick search might help find a better way to solve this problem.

See the SQL Server example [here](https://stackoverflow.com/questions/10404348/sql-server-dynamic-pivot-query).

### Development & debugging approach

Debugging is a big part of working with SQL. Regardless of whether it’s a piece of code you or somebody else has written, having the right approach might help quite a bit in getting to the root cause.

* Start small: work with a subset of data you’ve comfortable with. Understand better the shape of the data, whether it is clean or not, and execute pieces of the bigger query bit by bit.
    
* Debug single examples: when performing calculations, start with a particular observation (for example a person or order)
    
* Work at the right granularity: shape the data based on the task the query needs to solve. If you’re calculating country metrics per month, the intermediate steps need to be at the same granularity **before joining them all together**.
    

### Materialize if you reuse (and if you can)

When working with results sets that are reused multiple times in the same query (or even in multiple queries), consider materializing that data to avoid unnecessary computations. You can use the tools at hand in your SQL implementation, such as a temporary table or a regular table.

### Use DISTINCT and UNION the right way

De-duplicating data is undoubtedly very important, and DISTINCT and UNION keywords are quite handy. But using them comes at a performance cost, so we need to be mindful of whether we need them or not.

* Use UNION ALL instead of UNION if the results set you are uniting are known to be different. This will save needless processing.
    
* There is no need to use a DISTINCT when we have a clear indication that each row is already unique
    
* In cases when it’s not clear what you are de-duplicating (i.e. multiple columns that contain or could contain duplicates in the future), opt for using an explicit de-duplication step, for example using ROW\_NUMBER.
    

### Use the full power of your SQL implementation (and its version)

While SQL has a standard, individual database engine implementations do not follow it always in the same manner. Therefore, when trying to solve a problem, always seek to understand how to solve the problem.

Regularly check your product’s documentation for new additions that might ease your life. I for one recently discovered that [recursive CTEs in BigQuery have now been added in Preview](https://cloud.google.com/bigquery/docs/reference/standard-sql/query-syntax#with_clause).

### Conclusion

This is certainly a non-exhaustive list of SQL best practices, and there are cases where the requirements or the environment might dictate doing otherwise. As usual, as with all tips, we should always weigh in on a case-by-case basis and get things done. All in all, I hope that the above quick tips are going to be useful in your day-to-day work.

Happy SQLing!

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*