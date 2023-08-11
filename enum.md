---
layout: default
title: Enum
nav_order: 8
has_children: false
permalink: enum
---

## **Enum**
Utilize enums to avoid hardcoding values and create clear, maintainable code.

#### Usage :
Generate an enum class:
```
php artisan make:enum UserTypes
```
Define enum values:
```php
namespace App\Enums;

class UserTypes extends Enum
{
    public const ADMIN = 'admin';
    public const STUDENT = 'student';
}
```
methods:
```php
UserTypes::getAll() //get all types 
UserTypes::isValid($value) //to check if this value exists in the enum
UserTypes::toArray() //to get all enums as key and value
```
----

[^1]: [It can take up to 10 minutes for changes to your site to publish after you push the changes to GitHub](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll#creating-your-site).
