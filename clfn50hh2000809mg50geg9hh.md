---
title: "Extracting Twitter data using Python"
seoTitle: "Extracting Twitter Data using Python"
seoDescription: "Learn to extract Twitter data using Python in this tutorial"
datePublished: Mon Aug 19 2019 21:17:27 GMT+0000 (Coordinated Universal Time)
cuid: clfn50hh2000809mg50geg9hh
slug: extracting-twitter-data-using-python
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/hvSr_CVecVI/upload/659be6eb5aecc60b71f53c014032c1bb.jpeg
tags: twitter, python, pandas

---

Twitter is currently one of the most widely used social networks — 330 million people were using it monthly in Q1 2019. It may not have the explosive growth it had a couple of years ago, but it’s certainly a place where businesses and public persons engage with their audiences, important messages are shared in near-real time and, as recent events show, even politics is done.

Businesses and other actors have long understood the power that data from Twitter has. A typical example we could think of is trading firms. Given the fast-paced and concise format of messages shared, it is a nice tool that could be used to gather signals that could impact the stock market. A CEO commending a product or service? A partnership could be in the making. Multiple complaints from users about building issues in a new device? Bad news for the hardware vendor. So Twitter data does have a business use case.

In this three-part series, we’ll look into a Proof of Concept for extracting, transforming and understanding Twitter data relevant to a specific topic.

If you wish to follow along, please refer to the GitHub repository containing the full [Jupyter notebook for this series](https://github.com/cnstlungu/incubator/tree/master/Python/Exploring%20Twitter%20Data%20using%20Python).

### Setup

We’re going to use Python 3.7 and a few specialized libraries to get this done.

But first, we’ll need to obtain the necessary credentials from Twitter. This is done [here](https://developer.twitter.com/en/apps). After filling in the appropriate information, we should have the following:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563440222/b130ee67-eae9-47f8-b6a0-6b157f6759d3.png align="left")

Once we have the *API key*, *API secret key*, *Access token* and *Access token secret*, we can process to extract data from Twitter. We’re going to use the Twitter Search API to get our data.

Before we proceed, there’s another thing we should bear in mind though. This is an interface offered by Twitter that has [multiple tiers](https://developer.twitter.com/en/docs/tweets/search/overview), including the (free) Standard one we’re going to use. Its limitations are, as of writing this article, described as follows:

> This search API searches against a sampling of recent Tweets published in the past 7 days. Part of the ‘public’ set of APIs.

Nevertheless, this should be enough for our purposes.

### Getting Twitter data

Moving forward, we could either decide between making the API calls directly or using a library that will do so for us. Given the vast choice the Python ecosystem gives us, we’re going to use [TwitterSearch](https://pypi.org/project/TwitterSearch/), which should help us get moving quicker.

After installing TwitterSearch, we’re ready to go.

```bash
pip install TwitterSearch
```

Let’s import the necessary objects and instantiate the TwitterSearch object using the credentials Twitter has set up for us. In this case, I’ve set up a file that will store them.

We’ll now need to create a Search Order against the Search object we’ve defined above.

In this case, we’ve decided to analyze the messages concerning UK’s upcoming exit from the European Union, colloquially known as Brexit. We’re going to analyze tweets in English.

Now we have a list of tweets, which look like the one below.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563441956/b6681128-eccd-42f1-a448-768c0d6e9f72.png align="left")

We could see that we have a nested dictionary-like structure containing other dictionaries and lists. This needs to be flattened out so we could analyze data more efficiently. The [pandas](https://pandas.pydata.org/) library will facilitate this.

Here we’ve imported pandas and used the *json\_normalize* method to transform our list of results into a pandas *DataFrame — a two-dimensional tabular data structure.*

Also, here’s a quick view of our data:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563443751/82f31faf-4a7d-46b4-90dc-8ae168d304c2.png align="left")

To give a more meaningful identifier to each row than the currently used automatically generated row number, we’re going to use the unique tweet id column. We’re also going to drop the *id\_str* column since it’s the string representation of the same tweet id and is thus redundant.

Also, let’s look at how much data we’ve got. This will return (no\_of\_rows (tweets), no\_of\_columns (features/variables) ). So we’re currently looking at 18000 tweets with 326 attributes we could analyze.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563445287/1e7144d8-9641-4c6c-8cae-ca3a499c9724.png align="center")

A view of a subset of columns would be useful here. Let’s look at the date the tweet was created, the user screen name and the text of the tweet. These are only 3 of the several hundred columns available.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563446765/a7c11115-4b98-429f-9319-3d02f20f14d9.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563448358/7303d5c5-134c-42e8-971a-7da0bedc634e.png align="left")

#### Wrapping up

In this first post of the series we’ve looked at setting up our Twitter developer credentials, used the *TwitterSearch* Python package to extract tweets about Brexit and also used the *pandas* library to flatten (unpack) our results.

In the upcoming articles in this series, we’ll do further transformations of the data we’ve extracted and touch on the notions of Natural Language Processing and Sentiment Analysis.

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*