---
title: "Why you should care about VS Code Remote Development"
seoTitle: "Benefits of VS Code Remote Development"
seoDescription: "Discover the benefits of VS Code Remote Development and enhance your workflow with efficient resource management using SSH and remote servers"
datePublished: Tue Nov 12 2024 22:32:25 GMT+0000 (Coordinated Universal Time)
cuid: cm3f12hyk00010al91fhhcojg
slug: why-you-should-care-about-vs-code-remote-development
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/ERL-cQpwb18/upload/7fc48cce5d041bbe3e8e872e89d212b8.jpeg
tags: vscode, data-engineering, vscode-extensions

---

Maybe save a bit on that next expensive laptop upgrade?

Over the weekend, I worked on some small personal projects and decided to try out remote development using SSH and Visual Studio Code.

I have an 18 GB M3 Pro MBP, which is acceptable, but it’s not a whole lot when working with multiple containers. Luckily, I also have a pretty powerful (32 GB RAM/ Ryzen 9 5900HX) mini-PC that’s been collecting dust, so I thought I’d turn it into a Linux server—and effectively, a development box. I'm also more familiar with Ubuntu than I'm with the Mac.

I connected it directly to the router via cable for faster speeds and then set up ssh. With the remote dev pointed to the minipc in VSCode, while using my laptop it 100% felt like I was working locally, even though the heavy lifting was happening on the mini-PC.

The port forwarding makes it all pretty seamless, forwarding the ports from the server to my laptop, so you can just use your local browser.

What also I found cool was that I could still use all my VS Code extensions, like those for Docker or Python, just as I normally would.

With this setup, my laptop is essentially just the "control center"—all the processing happens on the mini-PC, so my laptop stays fast and cool.  
In short, all the development happens on my laptop, but the resource consumption is offloaded to my server.

![](https://miro.medium.com/v2/resize:fit:1400/0*pCOfUhYuDOs2Bjot align="left")

*Found it useful? Subscribe to my Analytics newsletter at* [https://www.notjustsql.com](https://www.notjustsql.com/) *.*