# Migration Guide: v2.x to 3.0.0

This guide details the steps required to migrate your application from `essa/api-tool-kit` v2.x to 3.0.0.

## Table of contents

---

## 1. Requirements Update

Version 3.0.0 requires:
- **PHP**: ^8.2
- **Laravel**: ^11.0 | ^12.0

Update your `composer.json` and run `composer update`.

---

## 2. Native Enums Migration

The legacy `Essa\APIToolKit\Enum\Enum` class has been removed. You must migrate to native PHP 8.1 enums.

### Step-by-step Migration:
1. Change `class MyEnum extends Enum` to `enum MyEnum: string`.
2. Use the `Essa\APIToolKit\Enum\EnumHelpers` trait.
3. Replace `public const NAME = 'value';` with `case Name = 'value';`.

**Example:**
```php
// Before
class UserType extends Enum {
    public const ADMIN = 'admin';
}

// After
enum UserType: string {
    use EnumHelpers;
    case Admin = 'admin';
}
```

---

## 3. Exception Handling

The `Essa\APIToolKit\Exceptions\Handler` class has been removed.

### For Laravel 11+:
Register the toolkit's exception renderers in `bootstrap/app.php`:

```php
use Essa\APIToolKit\APIToolKit;

->withExceptions(function (Exceptions $exceptions) {
    APIToolKit::registerExceptionRenderers($exceptions);
})
```

---

## 4. ApiResponse Changes

### Method Renaming
- `ResponseValidationError()` has been renamed to `responseValidationError()` (camelCase) to align with PSR-12 and other trait methods.

### Method Removal
- `responsePaginated()` has been removed. Use the `dynamicPaginate()` macro on your Eloquent models instead.

---

## 5. ConsumesExternalServices

The trait now uses the Laravel `Http` facade. If you were overriding internal Guzzle methods, you may need to refactor your implementation to use the `Http` facade's hooks or configuration options.

---

## 6. Configuration Update

A new `max_pagination_limit` option is available. Publish the updated config to use it:

```bash
php artisan vendor:publish --tag="config" --force
```
