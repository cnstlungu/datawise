---
title: "Understanding Generators in Python 🐍"
datePublished: Mon Sep 25 2023 21:12:57 GMT+0000 (Coordinated Universal Time)
cuid: clmzdxmwz000009jwb2eo08a9
slug: understanding-generators-in-python
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/8jNATlZXhgk/upload/0bb51cdd853a6026a281b1dbced665ab.jpeg
tags: programming-blogs, python, data-structure-and-algorithms

---

Generators are an important concept in Python. They are functions that produce a sequence of values when iterated over.

They provide an iterable (just like lists or tuples) but with a key difference - generators don't store all of their values in memory at once. They produce each value on-the-fly, as you iterate over them, so they're great to use when working with large datasets. And crucial to know about as a Data Engineer.

A generator is defined by using yield instead of return in a function.

In short: generators are:  
\- lazy (items are produced one by one when requested)  
\- stateful between calls (you can pick up where you left off using next() )  
\- immutable (the sequence produced cannot be modified)  
\- single-use (you can iterate through it only once)

![](https://miro.medium.com/v2/resize:fit:2000/0*dsHpSxwqoIcdRmkw align="left")

TL;DR When handling large, streaming or single-use collections, consider using generators. 💡

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*