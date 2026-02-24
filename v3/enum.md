---
layout: default
title: Enum
nav_order: 8
parent: V3 (Latest)
has_children: false
permalink: v3/enum
---
# Enum
{: .no_toc }

Enums provide a structured and consistent way to manage and reference predefined values in your application. The toolkit offers two approaches: **native PHP enums** (recommended) and a legacy class-based approach.

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Native PHP Enums (Recommended) <span class="label label-green">New in v2.3</span>

Since PHP 8.1, you can use native backed enums with the `EnumHelpers` trait for a type-safe, modern approach:

```php
namespace App\Enums;

use Essa\APIToolKit\Enum\EnumHelpers;

enum UserTypes: string
{
    use EnumHelpers;

    case Admin = 'admin';
    case Student = 'student';
}
```

### Available Methods

The `EnumHelpers` trait provides the following methods:

| Method            | Description                                          | Example Output                                         |
|:------------------|:-----------------------------------------------------|:-------------------------------------------------------|
| `values()`        | Get an array of all enum values                      | `['admin', 'student']`                                 |
| `names()`         | Get an array of all enum case names                  | `['Admin', 'Student']`                                 |
| `toArray()`       | Get an associative array of names to values           | `['Admin' => 'admin', 'Student' => 'student']`         |
| `isValid($value)` | Check if a value is valid for this enum              | `true` or `false`                                      |
| `fromValue($value)` | Get the enum case for a value, or null             | `UserTypes::Admin` or `null`                           |

### Example

```php
use App\Enums\UserTypes;

// Check if a value is a valid enum value
$isStudent = UserTypes::isValid('student'); // Returns true
$isUnknown = UserTypes::isValid('unknown'); // Returns false

// Get an array of all enum values
$allUserTypes = UserTypes::values(); // Returns ['admin', 'student']

// Get all case names
$names = UserTypes::names(); // Returns ['Admin', 'Student']

// Get an associative array
$map = UserTypes::toArray(); // Returns ['Admin' => 'admin', 'Student' => 'student']

// Get enum case from value
$type = UserTypes::fromValue('admin'); // Returns UserTypes::Admin
$invalid = UserTypes::fromValue('unknown'); // Returns null

// Use in match expressions (native PHP feature)
$label = match($type) {
    UserTypes::Admin => 'Administrator',
    UserTypes::Student => 'Student User',
};

// Use in type hints (native PHP feature)
function assignRole(UserTypes $type): void {
    // $type is guaranteed to be a valid UserTypes value
}
```

### Migrating from Legacy Enums

If you're currently using the class-based `Enum`, migrating to native enums is straightforward:

```php
// Before (deprecated):
class UserTypes extends Enum
{
    public const ADMIN = 'admin';
    public const STUDENT = 'student';
}

// After (recommended):
enum UserTypes: string
{
    use EnumHelpers;

    case Admin = 'admin';
    case Student = 'student';
}
```

**Key differences:**
- `getAll()` → `values()`
- `getConst()` → `names()`
- `toArray()` → `toArray()` (same name)
- `isValid($value)` → `isValid($value)` (same name)
- `getValue($const)` → `fromValue($value)`
- Constants use `case` keyword instead of `const`

---

### Legacy Enum Class (Deprecated)

{: .warning }
The class-based `Enum` is deprecated since v2.1 and will be removed in v3.0. Please migrate to native PHP enums with the `EnumHelpers` trait above.

#### Generating a Legacy Enum Class
```
php artisan make:enum UserTypes
```

#### Define enum values
```php
namespace App\Enums;

class UserTypes extends Enum
{
    public const ADMIN = 'admin';
    public const STUDENT = 'student';
}
```

Legacy methods: `getAll()`, `isValid($value)`, `toArray()`, `getConst()`, `isValidConst($value)`, `getValue($const)`.

----

[^1]: [It can take up to 10 minutes for changes to your site to publish after you push the changes to GitHub](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll#creating-your-site).
