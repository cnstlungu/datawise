---
title: "Using TUPLES in Python"
datePublished: Tue Sep 12 2023 09:27:46 GMT+0000 (Coordinated Universal Time)
cuid: clmg40otl001209jicbn64aop
slug: using-tuples-in-python
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/6jpdeeA2GBU/upload/bd3b3f95d2c90f48624c3b6e3fd168c5.jpeg
tags: programming-blogs, python, data-structure-and-algorithms

---

Continuing my posts about Python collections ([see post about sets](https://datawise.dev/using-sets-in-python)), let's look at another important data structure in Python - the tuple.

So when is it used and how does it differ from a list?

🌟 Strengths of Tuples:  
\- Immutable: Once created, they cannot be modified. This makes them hashable and usable as keys in dictionaries.  
\- Memory Efficient: Tuples are generally more memory-efficient than lists.  
\- Safety: Since they are immutable, there’s no risk of unintended side-effects when passing them around in functions.

🚫 Weaknesses of Tuples:  
\- Limited Flexibility: You can't add, remove, or modify elements after creation.  
\- Fewer Methods: They come with fewer built-in methods compared to lists.

🔍 When to use Tuples:  
\- When you need a collection of data that shouldn't change, like the days of the week or coordinates of a point.  
\- When you want to ensure data integrity and prevent accidental modifications.  
\- As keys for dictionaries.

✨ Differences from Lists:  
\- Mutability: Lists are mutable, tuples are not.  
\- Syntax: Lists use square brackets \[\] and tuples use parentheses ().  
\- Methods: Lists have several methods like append(), remove(), and extend(), which tuples do not (given their immutable nature).

```python
# Creating a Tuple
container_size = (5.0, 10.0)

# Accessing Elements
print(container_size[0])  # Outputs: 5.0

# Tuples in Dictionaries
locations = {(40.7128, -74.0060): 'New York', (51.5008, -0.1177): 'London'}

# List vs Tuple
example_list = [1, 2, 3]
example_type = (1, 2, 3)
example_list[1] = 4  # Valid
# my_tuple[1] = 4  # Throws an error
```

Tuples are great in their domain of applications! But like every tool, they have their place. Know when to use them over lists and leverage their strengths.

Happy coding! 🚀

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://www.notjustsql.com)*.*