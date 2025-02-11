---
title: "Why basic roles in BigQuery are a bad idea"
datePublished: Sat Jun 08 2024 18:15:11 GMT+0000 (Coordinated Universal Time)
cuid: clx6fqxyo00000ajoglyvh7j6
slug: why-basic-roles-in-bigquery-are-a-bad-idea
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/qD5Err_lJ5Y/upload/f0a51805c69113f2164f3c9b29547ac0.jpeg
tags: security, databases, google-cloud, sql, bigquery

---

> Paul Atreides: "He who can destroy a thing, controls a thing".

Remember to avoid as much as possible using the basic roles in BigQuery such as Owner, Editor or Viewer.

It may sound 'easier' to manage access using them, but it's a bad idea.

They make way for a number of problems:

* overly broad permissions: Editor = several thousand permissions, including read / write on ALL datasets, of course very far from the least privilege principle
    
* no granularity: not much wiggle room between these 3 roles
    
* security risk: one compromised Editor means a lot of trouble
    
* compliance: it's also a bad idea because it can land you in hot water with privacy regulations😁
    
* What to do instead:
    
* use one of many predefined roles that grant granular access to perform a specific set of tasks
    
* if you don't find the one you need (and the combination of multiple predefined ones that cover your use-case is too vast), you can create a custom role, bundling together minimum amount of rights you need to perform a particular task
    
* again, follow the principle of least privilege
    
* regularly review who has privilege to do what and why they need it, then clean up
    
* remember that you can also enforce dataset, table and even column/row-level security for a even more granular control
    
* use service accounts with minimal rights to handle processes
    
* use groups for easier management of privileges for a particular role (in a team) or function
    

*Found it useful? Subscribe to my Analytics newsletter at* [*notjustsql.com*](https://notjustsql.com)*.*