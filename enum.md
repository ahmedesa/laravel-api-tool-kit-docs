---
layout: default
title: Enum
nav_order: 8
has_children: false
permalink: enum
---

## **Enum**
The Enum class provides a convenient way to work with enumerations, allowing you to define a set of named constants that represent distinct values. By using enums, you can eliminate hardcoded values in your code and ensure consistency and maintainability.
### Generating an Enum Class
To create a new enum class, you can use the make:enum Artisan command:
```
php artisan make:enum UserTypes
```
This command generates an enum class named UserTypes in the App\Enums namespace. You can replace UserTypes with your desired enum name.

### Define enum values
```php
namespace App\Enums;

class UserTypes extends Enum
{
    public const ADMIN = 'admin';
    public const STUDENT = 'student';
}
```
The Enum class provides several methods to work with enums:
- `getAll()` Get an array containing all enum values.
- `isValid($value)` Check if a given value exists as a constant in the enum.
- `toArray()` Get an associative array containing all enum constants as keys and their respective values.

### Example
Here's an example of using the UserTypes enum:

```php
use App\Enums\UserTypes;

// Check if a value is a valid enum value
$isStudent = UserTypes::isValid('student'); // Returns true

// Get an array of all enum values
$allUserTypes = UserTypes::getAll(); // Returns ['admin', 'student']

// Get an array of enum constants
$enumConstants = UserTypes::toArray(); // Returns ['ADMIN' => 'admin', 'STUDENT' => 'student']
```
### Conclusion:
Enums provide a structured and consistent way to manage and reference predefined values in your application. By using the Enum class, you can create organized and maintainable code that avoids hardcoded values and promotes readability and consistency throughout your project.

----

[^1]: [It can take up to 10 minutes for changes to your site to publish after you push the changes to GitHub](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll#creating-your-site).
