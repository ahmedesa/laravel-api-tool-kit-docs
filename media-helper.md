---
layout: default
title: Media Helper
nav_order: 7
has_children: false
permalink: media-helper
---
## **Media Helper**
The Media Helper simplifies file uploading and deletion processes:
#### Usage :

Upload a file:

```php
$filePath = MediaHelper::uploadFile($file ,$path); 
```
Delete a file:
```php
MediaHelper::deleteFile($path); 
```
Upload multiple files:
```php
$filesPaths = MediaHelper::uploadMultiple($files ,$path); 
```
Upload base64 image:
```php
$imagePath = MediaHelper::uploadBase64Image($encodedImage ,$path); 
```

[🔝 Back to contents](#contents)

## **Enum**
Utilize enums to avoid hardcoding values and create clear, maintainable code.

#### Usage :
Generate an enum class:
```
php artisan make:enum UserTypes
```
Define enum values:
```php
namespace App\Enums;

class UserTypes extends Enum
{
    public const ADMIN = 'admin';
    public const STUDENT = 'student';
}
```
methods:
```php
UserTypes::getAll() //get all types 
UserTypes::isValid($value) //to check if this value exists in the enum
UserTypes::toArray() //to get all enums as key and value
```

[🔝 Back to contents](#contents)

----

[^1]: [It can take up to 10 minutes for changes to your site to publish after you push the changes to GitHub](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll#creating-your-site).
