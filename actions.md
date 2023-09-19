---
layout: default
title: Actions
nav_order: 6
has_children: false
permalink: actions
---

# Actions
{: .no_toc }

The Actions feature employs the command design pattern to encapsulate business logic within distinct and organized classes. This approach enhances code structure, readability, and maintainability in your Laravel application.

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Generating an Action Class
To create an action class, you can utilize the make:action Artisan command:

```
php artisan make:action CreateCar
```
This command generates an action class named `CreateCar` in the `App\Actions` namespace. Replace `CreateCar` with the desired action name.
### Defining Business Logic
After generating the action class, define your business logic within the execute method:

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
Within the execute method, you can encapsulate any complex business logic related to the action. This isolation promotes separation of concerns and maintainability.

### Utilizing Dependency Injection
To use the action class effectively, it's recommended to apply dependency injection. You have several options for utilizing the action class across your application.

#### Using Laravel Application Container
You can directly resolve and execute the action from the Laravel application container:
```php
app(CreateCar::class)->execute($data);
```
#### Injecting Action in Constructor
Inject the action class into a class's constructor to enable its usage within that class:
```php
private $createCarAction ;

public function __construct(CreateCar $createCarAction)
{
    $this->createCarAction=$createCarAction;
}

public function store(Request $request)
{
    $this->createCarAction->execute($request->all());
}
```
#### Injecting Action in Controller Function
Inject the action class directly into a Laravel controller function for usage:

```php
public function store(CreateCar $createCarAction)
{
    $createCarAction->execute($data);
}
```
### Benefits of Actions
By using the "Actions" feature, you can achieve the following benefits:

- **Clean and Organized Code** Business logic is encapsulated within distinct classes, improving code structure and readability.
- **Separation of Concerns** Business logic is separated from controllers and models, promoting a modular architecture.
- **Reusability** Actions can be reused across different parts of the application, reducing code duplication.

{: .note }
you can check this article to understand how Laravel’s IoC Container works [here](https://stefan-brankovikj.medium.com/laravels-ioc-container-and-dependency-injection-decoded-4529719c7fa3).


### Conclusion:
The Actions feature is a valuable tool for structuring and managing business logic within your Laravel application. Whether you're creating complex processes or handling straightforward tasks, this pattern empowers you to create organized, maintainable, and efficient code. Utilize dependency injection and choose the approach that best suits your application's needs to seamlessly integrate actions into your project

----
