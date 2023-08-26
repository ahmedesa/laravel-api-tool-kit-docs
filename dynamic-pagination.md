---
layout: default
title: Dynamic Pagination
nav_order: 3
has_children: false
permalink: dynamic-pagination
---
# Dynamic Pagination
{: .no_toc }

Dynamic Pagination provides you with the flexibility to control the number of results displayed per page in your API responses. This feature allows you to tailor the pagination behavior according to your application's needs.

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Paginating with Default Settings

To paginate results with the default configuration (20 items per page), you can simply call the `dynamicPaginate()` method on your model:

```php
$users = User::dynamicPaginate();
```
This will paginate the results and return a subset of users with a default of 20 users per page.

### Retrieving All Records Without Pagination

If you want to retrieve all records without applying pagination, you can use the `pagination` parameter with the value `'none'` in your request:
```
GET api/users?pagination=none
```
This will retrieve all users without any pagination applied.

### Customizing Pagination Per Page

You can customize the number of items per page by using the per_page parameter in your request:
```
GET api/users?per_page=10
```
In this example, the response will include 10 users per page.

### Changing Default Pagination Value

The default pagination value (number of items per page) can be configured in the `config/api-tool-kit` file. By default, it's set to 20 elements per page. To change this default value, modify the `default_pagination_number` configuration setting.
```php
[
    'default_pagination_number' => 20,
]
```
### Conclusion:

Dynamic Pagination empowers you to control the presentation of results in your API responses. Whether you want to stick with defaults or customize the pagination behavior, this feature gives you the flexibility to adapt to different scenarios and user requirements seamlessly. Use the provided methods and configuration settings to implement efficient and user-friendly pagination in your application.

----

[^1]: [It can take up to 10 minutes for changes to your site to publish after you push the changes to GitHub](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll#creating-your-site).
