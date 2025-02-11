---
title: "Dictionary Unpacking in Python"
datePublished: Fri Sep 08 2023 13:49:15 GMT+0000 (Coordinated Universal Time)
cuid: clmanljwi000e09l68xor9q3o
slug: dictionary-unpacking-in-python
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/GopRYASfsOc/upload/7d3e87c4c16d470c132969f39293a6f9.jpeg
tags: programming-blogs, python, programming-tips

---

One of the most versatile aspects of Python dictionaries is the ability to unpack them. Ever wondered how to use dictionary values as function arguments?

Simply employ the \*\* operator\*\*:

```python
def greet(name, age):
    return f"Hello {name}, you're {age} years old!"

data = {'name': 'Jane', 'age': 28}
print(greet(**data)) # This will print: Hello Jane, you're 28 years old!
```

Let's dive deeper into a practical use case:

Imagine making multiple API calls, where every call has a different template with a unique URL, endpoint, and parameters.

You'd need a systematic way to manage this. Here's when dictionary unpacking comes to the rescue.

%[https://gist.github.com/cnstlungu/4333aa644ee3420f67e0f18716d5f950] 

We're separating the templates and configuration and then leveraging dictionary unpacking for a flexible yet clean approach.

Stay tuned for more Python insights and best practices!

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*