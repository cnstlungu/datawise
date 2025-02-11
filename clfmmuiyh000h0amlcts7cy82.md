---
title: "Analyzing Reddit data using Scala, Spark and Spark-SQL"
datePublished: Sat Sep 10 2022 21:58:02 GMT+0000 (Coordinated Universal Time)
cuid: clfmmuiyh000h0amlcts7cy82
slug: analyzing-reddit-data-using-scala-spark-and-spark-sql-6246c75463c6
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/Oaqk7qqNh_c/upload/ab67b9d3b76a96e94895bc366d913542.jpeg
tags: big-data, spark, scala, reddit, sparksql

---

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563243992/027c7920-77a8-4687-b157-c42fc155e071.png align="center")

*A SQL query we can run against Reddit data thanks to Spark-SQL*

A while ago I was getting up to speed with Scala and Spark. Really powerful and interesting technology, I said to myself. So naturally, I’ve decided to test it out with a real use case.

One interesting piece of data to look at is Reddit. Given it’s a huge social network there’s room for many interesting projects with that data. I also found out that a website called [Pushshift](https://files.pushshift.io/reddit/) is archiving Reddit data. So I gave it a spin.

I was interested in extracting some posts and the comments attached to them. The resource has them organized by folder and then by monthly or daily snapshots. In this post, we’re going to look at how we can read this data and analyze it, and how to do it using Scala, Spark and Spark-SQL.

As usual, please refer to the GitHub repository if you’d like to follow along.

### Getting started

First, we’ve downloaded from the [Pushshift](https://files.pushshift.io/reddit/) website two daily extracts of data — one for the submissions and one for the comments associated with them. Another useful thing found there is the sample data, for both [submissions](https://files.pushshift.io/reddit/submissions/sample.json) and [comments](https://files.pushshift.io/reddit/comments/sample_data.json), which can be used to understand the structure of the data before processing it. As one could see from the files, these are JSONL (newline-delimited JSON files).

Another thing to notice is that the files provided are compressed (GZ or ZSTD), so we need to provide the appropriate options to allow for on-the-fly decompression or extract the archives beforehand. In my case the files were gz-ecrypted, so I had to add the **hadoop-xz** library to my **build.sbt** file.

```bash
libraryDependencies ++= Seq(
"org.apache.spark" %% "spark-core" % sparkVersion,
"org.apache.spark" %% "spark-sql" % sparkVersion,
"org.scalactic" %% "scalactic" % "3.2.9",
"org.scalatest" %% "scalatest" % "3.2.9" % "test",
"io.sensesecure" % "hadoop-xz" % "1.4"
)
```

### Data shape

Next, looking at the sample files provided, we’d need to pick what columns are relevant to what we want to analyze. Based on that, I’ve created one Case Class for both Submissions and Comments.

```scala
case class Submission(
selftext: String,
title: String,
permalink: String,
id: String,
created_utc: BigInt,
author: String,
retrieved_on: BigInt,
score: BigInt,
subreddit_id: String,
subreddit: String,
)

case class Comment(
author: String,
body: String,
score: BigInt,
subreddit_id: String,
subreddit: String,
id: String,
parent_id: String,
link_id: String,
retrieved_on: BigInt,
created_utc: BigInt,
permalink: String
)
```

We can then use the case classes to build the Spark Dataframe schemas.

```scala
val commentSchema = ScalaReflection.schemaFor[Comment].dataType.asInstanceOf[StructType]

val submissionSchema = ScalaReflection.schemaFor[Submission].dataType.asInstanceOf[StructType]
```

Then, the data frames can be created

```scala
val submissions = ss.read.schema(submissionSchema)
.option("io.compression.codecs","io.sensesecure.hadoop.xz.XZCodec")
.json(s"**$**assetsPath/RS_2018-02-01.xz").as[Submission]

val comments = ss.read.schema(commentSchema)
.option("io.compression.codecs","io.sensesecure.hadoop.xz.XZCodec")
.json(s"**$**assetsPath/RC_2018-02-01.xz").as[Comment]
```

We can now do a quick count to see how many entries we have for each data frame, representing one day’s worth of Reddit data.

```scala
//3194211 comments
println(comments.count())

//387140 submissions
println(submissions.count())
```

Now, let’s use Spark SQL to query this data. We start by aliasing the data frames as views, making them available in our Spark SQL context.

*submissions*.createOrReplaceTempView("submissions")

*comments*.createOrReplaceTempView("comments")

We can now run a SQL query against these two logical views. In the below query, we’re joining the submissions and the respective comments for that, keeping only those on the subreddit ‘worldnews’ (akin to a subforum) and filtering just one post id. We’re joining on the id/link\_id columns, with the ‘t3\_’ part being the post type, detailed [here](https://www.reddit.com/dev/api/).

```scala
ss.sql(
"""
|SELECT * FROM submissions s
| join comments c on replace(c.link_id,"t3_","") = s.id
| where s.subreddit='worldnews' and s.id = '7uktsn'
|
|
|""".stripMargin).show()
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563246344/87493dd0-866f-454d-87dc-1aa36c043be1.png align="left")

We can visit this post on the website by accessing the following URL.

[https://www.reddit.com/r/worldnews/comments/7uktsn](https://www.reddit.com/r/worldnews/comments/7uktsn)

We can also run a query to find out the average scores of the authors with the most posts during a particular day:

```scala
ss.sql(
"""
|SELECT author, COUNT(score), AVG(score)
|FROM submissions s
|WHERE subreddit='worldnews'
|GROUP BY author
|ORDER BY 2 DESC
|LIMIT 10
|
|""".stripMargin).show()
```

### Other considerations

* If you’d like to query ZSTD-compressed data, you might want to look at the following [example](https://gist.github.com/cnstlungu/3e284fc674f1550be150d9d970ff5a09).
    
* Be mindful of the scale and performance, as one month’s worth of data, of a dozen GB when archived, is a whopping 180+ GB of data when uncompressed. Test small, extract only what you need and learn about configuring and tuning Spark jobs (also applicable to me).
    
* Such an analysis would be neat inside a Jupyter Notebook. We can set up a Scala kernel for Jupyter. My workflow is [here](https://gist.github.com/cnstlungu/50a3a7d51a262677224e51e49803771e) and an example is [here](https://gist.github.com/cnstlungu/b58ccd3eaa07c368ff548295d014a2cf).
    

### Conclusion

In this short post, we’ve looked at leveraging Scala with Spark to read and process Reddit data using good old SQL, paving the way to an array of interesting applications. Thanks for reading!

*A kind reminder that the companion source code for this post is available on* [*Github*](https://github.com/cnstlungu/scala-spark-reddit-example)*.*

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*