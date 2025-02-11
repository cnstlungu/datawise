---
title: "Decorators in Python"
datePublished: Tue Dec 19 2023 22:38:33 GMT+0000 (Coordinated Universal Time)
cuid: clqcxf4c5000208jng5jd3kzd
slug: decorators-in-python
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/lHu6SF2Uar0/upload/4fcec339a540aa5539c8e00025d5b6d2.jpeg
tags: programming-blogs, python, developer, programming-tips

---

One of the important programming patterns is the decorator pattern.

What do decorators do? They modify a function's behavior, allowing us to enhance to add functionality without changing its structure. But how does it work in Python?

You might have noticed the syntactic sugar notation for the decorator - the so-called 'pie' notation: @.

```python
@decorator
def my_function():
    do something
```

Let's look at a quick practical example. We're going to define a 'polite' decorator that will modify announcements issued in a train station.

We will then decorate a function issuing such an announcement.

Here's how it would look like:

![](https://miro.medium.com/v2/resize:fit:1400/0*kQaafCRjVpWJZCJZ align="left")

Thanks for reading!

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*