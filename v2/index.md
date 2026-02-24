---
layout: default
title: V2 (Legacy)
nav_order: 1
has_children: true
permalink: v2/
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

#### Laravel 11+ (Recommended) <span class="label label-green">New in v2.3</span>

Use `APIToolKit::registerExceptionRenderers()` in your `bootstrap/app.php`:

```php
use Essa\APIToolKit\APIToolKit;

return Application::configure(basePath: dirname(__DIR__))
    ->withExceptions(function (Exceptions $exceptions) {
        APIToolKit::registerExceptionRenderers($exceptions);
    })
    // ... other configuration
    ->create();
```

This registers all exception renderers using Laravel 11+'s closure-based approach, converting exceptions into standardized JSON error responses.

#### Before Laravel 11 (Legacy) <span class="label label-yellow">Deprecated</span>

{: .warning }
The `Handler` class is deprecated since v2.3 and will be removed in v3.0. If you're on Laravel 11+, use the approach above.

For older Laravel versions, extend your exception handler from the `APIHandler` class:

```php
namespace App\Exceptions;

use Essa\APIToolKit\Exceptions\Handler as APIHandler;

class Handler extends APIHandler
{
}
```

Or for Laravel 11 without the new approach, bind in `AppServiceProvider`:

```php
use Essa\APIToolKit\Exceptions\Handler;
use Illuminate\Contracts\Debug\ExceptionHandler;

public function register(): void
{
    $this->app->bind(ExceptionHandler::class, Handler::class);
}
```

Both legacy approaches ensure that error responses adhere to the standardized format provided by the API toolkit.

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
