---
title: "Loading data from Google Cloud Storage into BigQuery using Cloud Workflows"
datePublished: Tue Oct 04 2022 22:52:23 GMT+0000 (Coordinated Universal Time)
cuid: clfmn9zn5000p0amlcs0yd6jz
slug: loading-data-from-google-cloud-storage-into-bigquery-using-cloud-workflows
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1679563240416/b007c020-2a49-4717-bf04-2d25ee490b89.png
tags: analytics, sql, bigquery, workflows

---

[Google Cloud Workflows](https://cloud.google.com/workflows/docs/overview) is a serverless orchestration platform that allows us to combine services into repeatable and observable sets of actions, connecting typically other GCP services. These are called, you guessed it, **workflows**.

While working as a Data Engineer and extensively using Apache Airflow (and its GCP implementation called Composer), I was a little skeptical in the beginning about what it is offering but came to appreciate its straightforwardness and simplicity.

In this quick exercise, we’re going to illustrate a simple use case — loading a CSV file from Google Cloud Storage into BigQuery.

#### Preparation work

Let’s set up the appropriate accounts and permissions. For this job, we’ve created a service account and assigned it the role “Big Query Job User”

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563216891/3f48c84e-e80d-4819-8253-67635a403512.png align="left")

Project roles for our service account

We’re also granted permission to the same service account to the Google Cloud Storage bucket from where we intend to load data from.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563217894/c2010698-cd54-4234-b6b5-29cd4fe7e901.png align="left")

Bucket permissions for the service account

Next, we need to create a destination BigQuery dataset and provide the service account “Big Query Data Editor” role on it. Note that the dataset needs to be in the same GCP region (or multi-region) as the bucket load our data into.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563219513/cacbea74-f1af-4713-899a-32380339fb52.png align="left")

BigQuery Destination dataset permissions

Now, let’s have a look at our file — a regular comma-delimited CSV, with the first row being the header row.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563221215/2c196477-3d11-45fe-9f3f-792bde88d2f1.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563223043/0808faae-2f34-4d11-af3b-29a37b2672db.png align="left")

By our legend, this file follows the below naming convention, with the first part being the date of the sale.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563224045/edb3dc9b-f029-439f-8e77-602bdbca889d.png align="left")

All good, now let’s get to the workflow itself.

#### Creating the workflow

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563225516/d8ce367c-8d18-49d0-99eb-cad8069a42be.png align="left")

In the dialog box we are presented, we give our workflow a name, pick the region and a service account (same as the one that we granted permissions above) to run the workflow under.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563226992/1c6e6097-666c-436a-9cc7-497d0f7ec553.png align="center")

If, let’s say, we’d like to read the file every day, that is — run the workflow on a particular schedule, we can create a Cloud Scheduler Trigger. This would automatically run the workflows at the given cadence.

Note that the project-level role “Workflows Invoker” needs to be attached to the service account triggering the Workflow.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563228829/f2e2539c-b076-443c-b051-1f2d4ed3e190.png align="center")

A workflow with a trigger would look as follows

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563230651/5d633430-f808-415b-92e9-71df00b5136b.png align="center")

#### Creating the steps

We now have the Workflow development window, where we can write the definition for our workflow in YAML-esque syntax. If you aren’t familiar with Workflow syntax, a good place to start is the [Workflows tutorials page](https://cloud.google.com/functions/docs/tutorials). Also, note the pane on the right side, illustrating our control flow

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563232844/992d6030-7432-4911-8ccc-07fc9e80ecf7.png align="left")

We now need the build the workflow logic. For this exercise, we’ll need to check the configuration options we can set up for the BigQuery job, documented at the following link

[**Method: googleapis.bigquery.v2.jobs.insert | Workflows | Google Cloud**  
\*Whether your business is early in its journey or well on its way to digital transformation, Google Cloud can help solve…\*cloud.google.com](https://cloud.google.com/workflows/docs/reference/googleapis/bigquery/v2/jobs/insert)

The easiest approach is to try to load data while using the schema auto-detect. Note the `autodetect: true` part in the load configuration.

The below code will:

* declare a resultsList List where we would accumulate job results
    
* create a BigQuery insert job with a set of provided arguments
    
* append the end state of the insert job to the list previously created
    
* print the list of job statuses us upon workflow completion
    

%[https://gist.github.com/cnstlungu/e7507e0b71660d94ca58d2fcd747d450] 

BigQuery has auto-detected the column types and loaded the data.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563234512/ac0099fb-ebed-4cff-819d-26d0dadad303.png align="left")

If we were to choose to provide the schema to the job, we can do the following:

%[https://gist.github.com/cnstlungu/befa89679a802613202c49c3f96dac92] 

Upon execution, this produces the following result.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563235798/8619136f-9ef0-46ed-9034-c2fa40ad0bcd.png align="left")

What if we have a slightly more advanced use case, and would like to read hundreds of files, which can be quite big, into a partitioned table? The code could look something like the one below.

Notice the following:

* timePartitioning by “DAY” based on field **date**
    
* the sourceUris now has a wildcard “\*” to catch all the files ending in “\_orders.csv”.
    

%[https://gist.github.com/cnstlungu/4c7237408a32161341f2e7ee2ade18cd] 

We now have a partitioned table

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563237454/eb3c9314-31bd-49b2-9e96-b35a530ff789.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563238680/0c905918-a5f6-43dc-80c2-8b56181ce1a7.png align="center")

#### Conclusion

As we have seen in this exercise, loading data from Google Cloud Storage into BigQuery using Cloud Workflows is quite straightforward and allows us to leverage the BQ API to build repeatable and low-overhead data pipelines in Google Cloud. Thanks for reading!

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*