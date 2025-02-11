---
title: "Installing Python packages with pip"
datePublished: Sat Jul 27 2024 20:56:09 GMT+0000 (Coordinated Universal Time)
cuid: clz4m2p3j000209la91vzgrs6
slug: installing-python-packages-with-pip
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/pdFMl6enmeo/upload/b49d01d705fec421cb297455f4bea64c.jpeg
tags: python, python3, data-engineering, dataengineering

---

Here are the basics you need to know about installing Python packages.

Apart from the built-in modules that come by default with the Python installation (the Standard Library), you need to install third-packages packages to be able to use them in your code (and of course import them).

You do so with a package manager. Perhaps the most widely known is **pip**, but there are other options like **poetry** or **uv**.

You can check more information about Python packages at [pypi.org](http://pypi.org)

Here's a quick list of common use cases:

`➡ pip install pandas # installs the package and its dependencies`

`➡ pip uninstall pandas # removes the package`

`➡ pip install --upgrade pandas # upgrades a package`

`➡ pip list # lists installed packages`

`➡ pip freeze > requirements.txt # saves the list of installed packages to a file so you can recreate the environment with the same packages next time you need it`

![](https://miro.medium.com/v2/resize:fit:1400/0*nyhP6cs6sj5nLpG6 align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://notjustsql.com)*.*