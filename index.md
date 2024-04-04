---
layout: default
title: Installation
nav_order: 1
has_children: false
permalink: /
---

## **Installation Guide**
To begin using the package, follow these steps to install it using Composer:

### Install The Package
```
composer require essa/api-tool-kit
```
This command will install the package in your Laravel project.
### Publish Configuration Files
To customize the behavior of the package, you can publish the configuration files. Run the following command:
```
php artisan vendor:publish --provider="Essa\APIToolKit\APIToolKitServiceProvider" --tag="config"
```
This command will copy the configuration files into your project's config directory, allowing you to modify settings as needed.

### Standardize Error Responses
#### Before Laravel 11
For consistent error responses, extend your application's exception handler from the `APIHandler` class provided by the package. In your `Handler.php` file located in the `app/Exceptions` directory, update it like so:

```php
namespace App\Exceptions;

use Essa\APIToolKit\Exceptions\Handler as APIHandler;

class Handler extends APIHandler
{
}

```
#### Laravel 11 
Starting from Laravel 11, the approach to handling exceptions has changed. Instead of extending the `Handler` class, you'll need to bind the exception handler in your `AppServiceProvider`. Here's how you can do it:

```php
<?php

namespace App\Providers;

use Essa\APIToolKit\Exceptions\Handler;
use Illuminate\Contracts\Debug\ExceptionHandler;
use Illuminate\Support\ServiceProvider;

class AppServiceProvider extends ServiceProvider
{
    public function register(): void
    {
        $this->app->bind(ExceptionHandler::class, Handler::class); // add this line 
    }
}
```
This integration ensures that error responses adhere to the standardized format provided by the API toolkit.

### Utilize the API Response Trait in your controllers

```php
namespace App\Http\Controllers;

use Essa\APIToolKit\Api\ApiResponse;

class Controller extends BaseController
{
    use ApiResponse;
}
```
For more details, refer to [API response](https://ahmedesa.github.io/laravel-api-tool-kit-docs/api-response)
