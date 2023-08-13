---
layout: default
title: Media Helper
nav_order: 7
has_children: false
permalink: media-helper
---
## **Media Helper**
The Media Helper is a utility class provided by the Essa\APIToolKit namespace that streamlines the file uploading and deletion processes for your Laravel application.
### Usage :
#### **Uploading a File**:

```php
use Essa\APIToolKit\MediaHelper;

$uploadedFilePath = MediaHelper::uploadFile($file, $path);
```
Parameters:
- **$file** An instance of Illuminate\Http\UploadedFile containing the file to be uploaded.
- **$path** The directory path where the file should be stored.

#### **Deleting a File**:
Remove a file using the deleteFile method.
```php
use Essa\APIToolKit\MediaHelper;

MediaHelper::deleteFile($filePath);
```
Parameters:
- **$filePath** The path of the file to be deleted.
  
#### **Uploading Multiple Files**:
You can upload multiple files simultaneously using the uploadMultiple method.
```php
use Essa\APIToolKit\MediaHelper;

$uploadedFilePaths = MediaHelper::uploadMultiple($files, $path);
```
Parameters:

- **$files** An array of Illuminate\Http\UploadedFile instances containing the files to be uploaded.
- **$path** The directory path where the files should be stored.
#### **Uploading Base64 Images**:
You can upload images in base64 format using the uploadBase64Image method.
```php
use Essa\APIToolKit\MediaHelper;

$encodedImage = 'data:image/png;base64,iVBORw0KG...'; // Replace with actual base64 image data
$path = 'uploads/images'; // Destination path

// Upload the base64 image and get the uploaded image path
$uploadedImagePath = MediaHelper::uploadBase64Image($encodedImage, $path);
```
Parameters:
- **$encodedImage** The base64-encoded image data.
- **$path** The directory path where the image should be stored.

### Conclusion:
The Media Helper simplifies common file uploading and deletion tasks in your Laravel application. Its methods are designed to make managing files more efficient and user-friendly. Use the provided methods to seamlessly integrate file handling capabilities into your project.

----
