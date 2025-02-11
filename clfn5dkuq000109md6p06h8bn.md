---
title: "An Intro to NLP and Sentiment Analysis using Python"
seoTitle: "Transform Twitter data using Python"
seoDescription: "Follow along this tutorial to find out how to Transform Twitter data using Python and Pandas"
datePublished: Mon Aug 26 2019 21:35:08 GMT+0000 (Coordinated Universal Time)
cuid: clfn5dkuq000109md6p06h8bn
slug: intro-nlp-sentiment-analysis-python
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/YPgTovTiUv4/upload/acde73dbfcfeb196587934b6ffcf7370.jpeg
tags: analytics, python, pandas, nlp

---

[In the first article of this series](https://hashnode.com/post/clfn50hh2000809mg50geg9hh), we’ve looked at the setup needed to tap into the Twitter APIs, how to search tweets about a certain topic (we picked Brexit given the overwhelming media coverage) and how to pre-process the data to get to a tabular form.

In this post, we’ll build on the foundation laid by that work and do further data processing and feature extraction. We’ll also introduce notions of Natural Language Processing and present a proof of concept for a sentiment analysis tool.

Again, please refer to the GitHub repository containing the full [Jupyter notebook for this series](https://github.com/cnstlungu/incubator/tree/master/Python/Exploring%20Twitter%20Data%20using%20Python) if you wish to follow along.

#### Processing the data

First, let’s have a look at where we left off in the previous part. Namely, let’s have a closer look at our text.

Since we’re looking at tweets, the *text* attribute of the tweet — the actual message tweeted — is one of the most important we have in our data set. We can now identify a couple of problems with the data:

* No guarantee that we’re looking at unique tweets (about their *text*). Viral messages might be retweeted dozens of times.
    
* Elements that don’t add value to the meaning of the tweet: punctuation marks and special characters, hyperlinks, Twitter handles, *stopwords*, metadata (such as the ‘RT’ for retweeted)
    

Let’s first remove duplicates. We’ll think of them as tweets with the same text as other tweets, for instance, multiple retweets of the same original tweet.

```python
df.drop_duplicates(subset='text',inplace=True)
```

Let’s inspect how many rows we’ve dropped by removing the duplicates. So, from a randomly-build dataset of 18000 tweets, we end up with 6389 unique tweets.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563453422/eb86270d-0d16-46b0-89db-3761e64d7ee1.png align="left")

before

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563455018/c97d8f59-924a-4ee0-8990-85b7c63ca6e8.png align="left")

after

Let’s proceed with our processing of the text. We’ll apply the following steps one by one:

* transform tweet text into lowercase
    
* remove Twitter handles
    
* remove hyperlinks
    
* remove non-alphanumeric characters such as punctuation marks
    
* remove whitespace
    

The next step would be removing the stopwords — auxiliary words that can be ignored. We’re going to use a predefined list of stopwords together with a couple of works such as retweet (‘rt’).

```python
from nltk.corpus import stopwords
additional  = ['rt','rts','retweet']
swords = set().union(stopwords.words('english'),additional)
```

Here’s a preview of the words we’re excluding:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563456004/23e26251-84fb-441d-90ae-f32ed189a202.png align="left")

A total of 182 words

```python
df['processed_text'] = df['text'].str.lower()\
          .str.replace('(@[a-z0-9]+)\w+',' ')\
          .str.replace('(http\S+)', ' ')\
          .str.replace('([^0-9a-z \t])',' ')\
          .str.replace(' +',' ')\
          .apply(lambda x: [i for i in x.split() if not i in swords])
```

Let’s apply the following transformation to remove stopwords from our processed text.

Another transformation could be stemming the words. Think about ‘play’, ‘played’, ‘plays’, ‘playing’. Since all of them represent the same idea, it would be nice to reduce them to the same concept and count them together.

```python
from nltk.stem import PorterStemmer
ps = PorterStemmer()
df['stemmed'] = df['processed_text'].apply(lambda x: [ps.stem(i) for i in x if i != ''])
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563457422/84f554df-5bde-4c4d-91a2-0f70a741bb89.png align="left")

The columns we’ve obtained through original tweet text transformation and its stemming will allow us to analyze the vocabulary used, look at what tare the recurring themes and identify the word most used.

We’ll now briefly look at analyzing the sentiment of these tweets.

#### Sentiment Analysis

Given the great number of the tweets one wouldn’t be able to read through them all to understand the general feeling of the public. Therefore, we’d require a more automated way to tell whether a given tweet is positively or negatively talking about the topic we’re interested in. A simple analyzer could look as follows:

* Create a dictionary of words, denoting various emotions or sentiments
    
* Score them accordingly: negative for the negative ones, positive for the positive ones. Say *horrific* is -5, *terrible* is -3, *bad* is -1 while *good* is +1, *great* +3 and *outstanding* + 5.
    
* For a given phrase, sum the scores up and see what score you’re getting.
    

That’s a basic sentiment analyzer. Fortunately, these tools already exist within the Python ecosystem and we could use them to do that for us. Namely, we’re going to use the Vader Sentiment Intensity Analyzer.

```python
import nltk.sentiment.vader as vd
from nltk import download
download('vader_lexicon')
sia = vd.SentimentIntensityAnalyzer()
```

We’re also going to use a word tokenizer, which will feed our words one by one to the Sentiment Analyzer.

```python
from nltk.tokenize import word_tokenize
df['sentiment_score'] = df['processed_text'].apply(lambda x: sum([ sia.polarity_scores(i)['compound'] for i in word_tokenize( ' '.join(x) )]) )
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563458485/af0ad2bb-8962-4c46-b985-4ae79f37620a.png align="left")

Of course, we should inspect the data in detail to see if we’re happy with the way the Polarity Scoring has assigned sentiments to our tweets.

Now, we will try to visualize the split between attributed sentiments. As we can see, the term is quite contradictory, with a slight advantage for the negative sentiment.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563460316/28d7db22-e644-434b-852e-4b936d4fa062.png align="left")

Unfortunately, some of the more negative opinions (&lt;-2) could not be reproduced here given the strong language used. We’re going to look more at sentiment in the next part of our series.

#### A closer look at our features

So by now, we know some of the transformations we can apply to our text and how to get a feel for the sentiment of the texts. But we could still mine more data from any of the 320+ attributes we have apart from the tweet text itself.

For example, from the **user.followers\_count** table we could understand which of our tweets belongs to a user that has a low, medium or high Twitter audience. We’ve divided the users into 3 buckets: less than 300 followers, between 300 and 10.000 followers and over 10.000 followers. A bigger sample size could also allow us to understand the size of the audiences the messages reach.

```python
df['user_audience_category'] = pd.cut(df['user.followers_count'],[0,300,10000,999999999],include_lowest=True,labels=['small','medium','wide'])
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679563461173/07d04a73-bda1-4ce9-b13d-64f2a0254834.png align="left")

#### Conclusion

This part of the series presented ways in which we can transform the text retrieved from Twitter, perform basic sentiment analysis as well as build new simple features from the data we already have.

In the following articles of this series, we’re going to look at ways we can analyze this data and present it to an interested group. Thanks for reading and stay tuned for the next posts.

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*