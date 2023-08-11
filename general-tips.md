---
layout: default
title: General tips
nav_order: 9
has_children: false
permalink: general-tips
---

## **General Tips**

Prefer throwing exceptions instead of directly returning JSON responses for better error handling.

Bad:

```php
public function index()
{
    if (auth()->user()->not_active ) {
        $this->responseUnAuthorized('you can not preform this action');
    } 
}
```
good

```php
public function index()
{
    if (auth()->user()->not_active ) {
        throw new AuthorizationException('you can not preform this action');
    } 
}
```
----

[^1]: [It can take up to 10 minutes for changes to your site to publish after you push the changes to GitHub](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll#creating-your-site).
