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
For consistent error responses, extend your application's exception handler from the `APIHandler` class provided by the package. In your `Handler.php` file located in the `app/Exceptions` directory, update it like so:

```php
namespace App\Exceptions;

use Essa\APIToolKit\Exceptions\Handler as APIHandler;

class Handler extends APIHandler
{
}

```
This integration ensures that error responses adhere to the standardized format provided by the API toolkit.
