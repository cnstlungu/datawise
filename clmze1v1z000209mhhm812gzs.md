---
title: "Python Showdown: Namedtuple vs SimpleNamespace vs DataClass"
datePublished: Mon Sep 25 2023 21:16:15 GMT+0000 (Coordinated Universal Time)
cuid: clmze1v1z000209mhhm812gzs
slug: python-showdown-namedtuple-vs-simplenamespace-vs-dataclass
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/foYl6lptLY8/upload/312b4cfd0c2e12b63953e0c4364b58ae.jpeg
tags: programming-blogs, python, data-structure-and-algorithms

---

Python users, ever needed a light data container (like a dictionary) but wanted to access members using the dot (.) notation?

There are a couple of options to choose from: namedtuple, SimpleNamespace  
and dataclass.

Here's how they all differ:

1️⃣ namedtuple: immutable, memory efficient, iterable and members can be accessed by index as well. Static and somewhat verbose.

2️⃣ simple\_namespace: mutable, uses more memory than namedtuple, not iterable nor indexable. Flexible and less verbose.

3️⃣ dataclass: can be mutable or not (controlled by `frozen` parameter), can set default attributes, has special methods like **repr** (how it's displayed) and **eq** (check if it's equal to another instance). Uses more memory and is relatively newly-introduced (Python 3.7).

![](https://miro.medium.com/v2/resize:fit:3686/0*RlfJs9l0AhBd6AJf align="left")

When to use which?  
➡ namedtuple: You need something light on memory and immutable

➡ simple\_namespace: You need flexibility to change the attributes or even  
add them dynamically with little boilerplate.

➡ dataclass: You want more flexibility and control.

🔔 Follow me for more insights on Python and Analytics. Thanks for reading!

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*