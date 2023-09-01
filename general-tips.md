---
layout: default
title: General tips
nav_order: 9
has_children: false
permalink: general-tips
---
# General Tips
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

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

### Optimizing Search Operations in Your Database

When implementing search functionality in your API with the [Query Filters](https://laravelapitoolkit.com/filters), iit's essential to consider its potential impact on your database performance. The typical %like% search, as demonstrated in the example, can be resource-intensive and may not be suitable for large-scale projects or databases with extensive data. Here are some important considerations and alternatives:
#### Database Performance
Query filters use the %like% approach, which can lead to slow query execution, especially when dealing with large datasets. It performs a full-text search across columns, making it less efficient for high-volume applications.
#### Alternatives
- **Laravel Scout** Laravel Scout is a powerful package that integrates with popular search engines like Algolia and Elasticsearch. It provides efficient full-text search capabilities and is well-suited -for applications with extensive search requirements.
- **Elasticsearch** Elasticsearch is a dedicated search engine that excels at handling complex search queries and large volumes of data. It offers advanced features like full-text search, faceted search, and real-time indexing.

By considering these alternatives, you can optimize your API's search functionality and ensure better performance, especially when dealing with substantial data loads.

----
