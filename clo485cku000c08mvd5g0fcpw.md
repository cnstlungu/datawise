---
title: "Importing Google Sheets into BigQuery"
datePublished: Tue Oct 24 2023 11:09:33 GMT+0000 (Coordinated Universal Time)
cuid: clo485cku000c08mvd5g0fcpw
slug: importing-google-sheets-into-bigquery
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/TisvwNLLWA4/upload/a19301b4e8f097180c32c1d68080b1c6.jpeg
tags: google-cloud, google-sheets, bigquery, google-drive

---

Spreadsheets are a central part of a modern workplace. Pretty much every office workplace uses one. It's also quite used for personal use cases. One such product is Google Sheets.

I use it for many things - organizing finance, planning travel itineraries, collecting data and expenses.

Today I want to illustrate how we can integrate data from Google Sheets to BigQuery.

In BigQuery, a Google Sheets page can be represented as an external table - a type of table where the data is stored outside of BigQuery.

### Where to use it?

I've seen them used for holding static (seed) data and mapping tables, an improvised Master Data Management of sorts, allowing analysts to edit data as business realities change.

### What to pay attention to?

* Security - who can view and edit Sheets
    
* History - how do you handle change in sheets? Do you need snapshots?
    
* Recovery - what if someone deletes data from the worksheet?
    

Let's see an example of how to set it up.

### Setting up a Google Sheet as an External Table

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698142062300/bd6670cf-76ec-4f70-bf45-9a7cb27b26d0.png align="center")

We start by adding a new data source.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698145294195/7d456086-6bf3-49da-83d1-0697a605ee71.png align="center")

We pick the **Google Drive** as the source.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698141989838/be0fc79f-3ad8-41c0-a281-b92b26378740.jpeg align="center")

We provide the necessary configuration:

* Google Sheets URL
    
* Destination Table: project, dataset, table name
    
* We provide the schema: column names and types
    
* We provided the number of header rows to be skipped
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698142025138/fc78e8d7-42b5-44fa-89d1-3082d802ac13.jpeg align="center")

After we hit ***Create Table*** the external table is created. We can verify that the data has been properly created.

* ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698142467225/7e2cd06c-0235-4a33-a31a-0c2ce9886f76.png align="center")
    

### Viewing the DDL of an (external) table

We might need to see the DDL (data definition language) statement for a table. This can be achieved using one of the INFORMATION\_SCHEMA tables.

Using the query below you can see how the (external in our case) table is defined.

```sql
SELECT
 table_name, ddl
FROM
 learning.INFORMATION_SCHEMA.TABLES;
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698142035903/480a04aa-8805-4d6c-bc00-24a025f0a451.jpeg align="center")

```sql
CREATE EXTERNAL TABLE `learning.example_table`
(
  FirstName STRING OPTIONS(description="First Name"),
  LastName STRING OPTIONS(description="Last Name"),
  City STRING OPTIONS(description="City"),
  Country STRING OPTIONS(description="Country")
)
OPTIONS(
  sheet_range="A1:D4",
  skip_leading_rows=1,
  format="GOOGLE_SHEETS",
  uris=["https://docs.google.com/spreadsheets/d/**edited_text**/edit#gid=0"]
);
```

Thanks for reading and keep enjoying SQL!

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*