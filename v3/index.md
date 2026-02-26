> [!IMPORTANT]
> **Upgrading from v2.x?** Please read the [Migration Guide](migration-guide) for breaking changes and upgrade steps.

## **Installation Guide**
To begin using the package, follow these steps to install it using Composer:

### Install The Package
```
composer require essa/api-tool-kit
```
This command will install the package in your Laravel project.

### Install AI Architectural Skill <span class="label label-green">New in v3.1</span>

Give your AI coding assistant a shared understanding of your architecture. One command installs **19 rule files** and **4 guided workflows** — every AI-generated file will match your standards from the first draft.

```bash
php artisan api-skill:install
```

The installer asks which AI tool you use (Claude Code, Cursor, GitHub Copilot, or Antigravity) and copies the skill to the correct location automatically.

> [!TIP]
> The AI Skill is the recommended way to generate code for projects using this package. It replaces the need for scaffolding generators by teaching your AI assistant the full architecture.

For the complete list of rules, workflows, and customization options, see the [AI Architectural Skill](ai-skill) section.

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

### Utilize the API Response Trait in your controllers

```php
namespace App\Http\Controllers;

use Essa\APIToolKit\Api\ApiResponse;

class Controller extends BaseController
{
    use ApiResponse;
}
```
For more details, refer to [API response](api-response)
