---
layout: default
title: Actions
nav_order: 6
has_children: false
permalink: actions
---

## **Actions**
Actions implement the command design pattern, providing a structured way to encapsulate business logic.
#### Usage :

Generate an action class:

```
php artisan make:action CreateCar
```

```php
<?php
namespace App\Actions;

class CreateCar
{
    public function execute($data)
    {
      //add business logic to create a car
    }
}
```
The best practice to use the action class is to use dependency injection

you have many options
1-use Laravel application container
```php
app(CreateCar::class)->execute($data);
```
2-inject it in the class in the constructor

```php
private $createCarAction ;

public function __construct(CreateCar $createCarAction)
{
    $this->createCarAction=$createCarAction;
}

public function doSomething()
{
    $this->createCarAction->execute($data);
}
```
3-inject the class in Laravel controller function

```php
public function doSomething(CreateCar $createCarAction)
{
    $createCarAction->execute($data);
}
```
[🔝 Back to contents](#contents)


----

[^1]: [It can take up to 10 minutes for changes to your site to publish after you push the changes to GitHub](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll#creating-your-site).
