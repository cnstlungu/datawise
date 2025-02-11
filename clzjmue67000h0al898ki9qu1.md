---
title: "A quick look at the json module in Python"
datePublished: Wed Aug 07 2024 09:14:14 GMT+0000 (Coordinated Universal Time)
cuid: clzjmue67000h0al898ki9qu1
slug: a-quick-look-at-the-json-module-in-python
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/fvMeP4ml4bU/upload/0eb0978fef1e70dc2db9b6cded76dbce.jpeg
tags: python, json, dataengineering

---

If you ever need to work with JSON files in Python, you're going to encounter the module with the same name.

It help encode to and decode from JSON. Here are the basics:

➡ json.load imports contents from a JSON file to a Python object, based on conversion rules (object -&gt; dict, array -&gt; list/tuple, string-&gt; str etc)

➡ json.dump performs the opposite operation - export to a file-like object

There are also the json.loads and json.dumps functions (notice the extra s) which apply to strings instead of files.

There's also the *json.tool*, which can validate and pretty-format a provided json file.

You can save that prettified json into another file, as follows:

`python -m json.tool ugly_format.json pretty_format.json`

![](https://miro.medium.com/v2/resize:fit:1400/0*CmsJRPuTkbV13MNz align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://notjustsql.com)*.*