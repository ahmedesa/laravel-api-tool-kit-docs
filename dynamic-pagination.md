---
layout: default
title: Dynamic Pagination
nav_order: 3
has_children: false
permalink: dynamic-pagination
---

## **Dynamic Pagination**
Use dynamic pagination to manage the number of results per page in API responses.

#### usage
To paginate results with the default of 20 items per page:
```php
$users = User::dynamicPaginate();
```
To retrieve all users without pagination:
```
\users?pagination='none'
```
To paginate with a custom number of items per page:
```
\users?per_page=10
```
by default, pagination is 20 elements per page you can change the default value from config/api-tool-kit

----

[^1]: [It can take up to 10 minutes for changes to your site to publish after you push the changes to GitHub](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll#creating-your-site).
