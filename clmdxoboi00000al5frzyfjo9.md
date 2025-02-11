---
title: "Using SETS in Python"
datePublished: Sun Sep 10 2023 20:54:39 GMT+0000 (Coordinated Universal Time)
cuid: clmdxoboi00000al5frzyfjo9
slug: using-sets-in-python
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/t5YUoHW6zRo/upload/a7a08b8f5e5e00ea1b0176197390ff0b.jpeg
tags: programming-blogs, python, data-structures

---

Using the right tool for the job is central to programming. This holds when considering what data structure to use for a particular problem.

Python offers a variety of built-in data structures, and one of the most versatile among them is the set. Let's explore its strengths, weaknesses, and ideal use cases.

✅ Strengths:  
\- Uniqueness: Sets automatically remove duplicates, ensuring each element is unique. You can convert a list into a set and back to a list to obtain a list of unique values in the original list.  
\- Fast Membership Testing: Checking if an item is in a set is much faster, typically constant time O(1), than in a list O(n).  
\- Set Operations: Supports union, intersection, difference, and more, making it powerful for mathematical operations.

❌ Weaknesses:  
\- Unordered: Sets do not maintain the order of elements.  
\- Immutable Elements: Only hashable (immutable) elements can be added to a set. So, lists can't be set elements, but tuples can.  
\- No Indexing: You can't access or modify an element of a set using an index or key.

🤔 When to Use:  
\- When you need to ensure elements are unique.  
\- When you want to perform set operations like union, intersection, etc.  
\- When you require fast membership testing.

```python

# Creating a set
vegetables = {"eggplant", "cucumber", "squash"}

# Adding an element
vegetables.add("potato")

# Test membership
print("potato" in vegetables) #True

# Removing duplicates from a list
unique_nums = set([1, 2, 2, 3, 4, 4, 5])
print(unique_nums) # {1, 2, 3, 4, 5}

# Set operations
a = {1, 2, 3}
b = {3, 4, 5}
print(a.union(b))  # {1, 2, 3, 4, 5}
```

In conclusion, the set container is a powerful tool in Python's arsenal. While it has its limitations, understanding when and how to use it can greatly enhance your coding efficiency!

👉 Follow me for more insights on Python, SQL and analytics!

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*