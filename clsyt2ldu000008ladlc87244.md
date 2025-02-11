---
title: "Using zip in Python"
datePublished: Fri Feb 23 2024 15:27:11 GMT+0000 (Coordinated Universal Time)
cuid: clsyt2ldu000008ladlc87244
slug: using-zip-in-python
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/plwud_FPvwU/upload/6cf85d119ee0acc0faa4a3048592ffee.jpeg
tags: programming-blogs, python, developer, python3, programming-languages

---

If you haven't encountered it already, note that zip is quite handy in Python.

It allows you to go through multiple iterables (such as lists, sets, tuples etc) at the same time, effectively "zipping" them into an iterator that will produce tuples of elements from each initial collection.

Worth keeping in mind that if the provided iterables' length differs, zip will stop when the shortest of them has reached its end.

Happy coding!

```python
integers = [1,2,3,4,5]

letters = ['a','b', 'c', 'd']

for pair in zip(integers, letters):
    print(pair)

# Prints:
# (1, 'a')
# (2, 'b')
# (3, 'c')
# (4, 'd')
```

*Found it useful? Check out to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*