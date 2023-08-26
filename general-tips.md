---
layout: default
title: General tips
nav_order: 9
has_children: false
permalink: general-tips
---
# Typography
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## **General Tips**

### Use Exceptions for Clear Error Handling
Prefer throwing exceptions instead of directly returning JSON responses. The package will catch the error and format the response automatically.

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
When the exception is thrown, the package will capture it and format the response. For instance, if you throw an `AuthorizationException`, the response JSON will look like this:
```json
{
    "errors": [
        {
            "status": 403,
            "title": "Forbidden",
            "detail": "you cannot perform this action"
        }
    ]
}
```
This approach ensures consistent error handling and standardized response formatting throughout your API.

----
