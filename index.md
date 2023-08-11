---
title: Laravel API tool kit
layout: Laravel API tool kit
---

## **Installation**
To get started, install the package using Composer:
```
composer require essa/api-tool-kit
```
To publish the configuration files, run:
```
php artisan vendor:publish --provider="Essa\APIToolKit\APIToolKitServiceProvider" --tag="config"
```
For standardizing error responses, extend your exception handler from the APIHandler class:
```php

namespace App\Exceptions;

use Essa\APIToolKit\Exceptions\Handler as APIHandler;

class Handler extends APIHandler
{
}

```

Utilize the API Response Trait in your controllers:

`App\Http\Controllers\Controller.php`:

```php
use Essa\APIToolKit\Api\ApiResponse;

class Controller extends BaseController
{
    use ApiResponse;
}
```
For more details, refer to [API response](#api-response)
----

[^1]: [It can take up to 10 minutes for changes to your site to publish after you push the changes to GitHub](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll#creating-your-site).

[Just the Docs]: https://just-the-docs.github.io/just-the-docs/
[GitHub Pages]: https://docs.github.com/en/pages
[README]: https://github.com/just-the-docs/just-the-docs-template/blob/main/README.md
[Jekyll]: https://jekyllrb.com
[GitHub Pages / Actions workflow]: https://github.blog/changelog/2022-07-27-github-pages-custom-github-actions-workflows-beta/
[use this template]: https://github.com/just-the-docs/just-the-docs-template/generate
