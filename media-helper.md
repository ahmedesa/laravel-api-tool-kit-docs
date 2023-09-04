---
layout: default
title: Media Helper
nav_order: 7
has_children: false
permalink: media-helper
---

# Media Helper
{: .no_toc }

The Media Helper is a utility class provided by the `Essa\APIToolKit` namespace that streamlines the file uploading and deletion processes for your Laravel application.

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Uploading a File

```php
use Essa\APIToolKit\MediaHelper;

$uploadedFilePath = MediaHelper::uploadFile($file, $path, $fileName = null, $withOriginalName = false);
```
Parameters:
- `$file`(UploadedFile):  An instance of Illuminate\Http\UploadedFile containing the file to be uploaded.
- `$path` (string): The directory path where the file should be stored.
- `$fileName` (string, optional): A custom filename to use for the uploaded file. If not provided, a filename will be generated automatically.
- `$withOriginalName` (bool, optional): If set to true, the file will be saved with its original name. Default is false.
  
### Deleting a File
Remove a file using the deleteFile method.
```php
use Essa\APIToolKit\MediaHelper;

MediaHelper::deleteFile($filePath);
```
Parameters:
- `$filePath` The path of the file to be deleted.
  
### Uploading Multiple Files
You can upload multiple files simultaneously using the uploadMultiple method.
```php
use Essa\APIToolKit\MediaHelper;

$uploadedFilePaths = MediaHelper::uploadMultiple($files, $path, $filesNames = null, $withOriginalNames = false);
```
Parameters:

- `$files` An array of Illuminate\Http\UploadedFile instances containing the files to be uploaded.
- `$path` The directory path where the files should be stored.
- `$withOriginalNames` (bool, optional): If set to true, the files will be saved with their original names. The default is false.
- `$filesNames` (array, optional): An array of custom filenames to use for the uploaded files. If not provided, filenames will be generated automatically.
  
### Uploading Base64 Images
You can upload images in base64 format using the uploadBase64Image method.
```php
use Essa\APIToolKit\MediaHelper;

$encodedImage = 'data:image/png;base64,iVBORw0KG...'; // Replace with actual base64 image data
$path = 'uploads/images'; // Destination path

// Upload the base64 image and get the uploaded image path
$uploadedImagePath = MediaHelper::uploadBase64Image($encodedImage, $path, $fileName = null);
```
Parameters:
- `$encodedImage` The base64-encoded image data.
- `$path` The directory path where the image should be stored.
- `$fileName` (string, optional): A custom filename to use for the uploaded image. If not provided, a filename will be generated automatically.
### Uploading to a Custom Disk
You can upload files to any configured disk using the disk method. If no disk is explicitly specified, the default disk will be used for the operation; otherwise, the specified disk will be used.

Example:


```php
// Upload a file to the 's3' disk
$uploadedFilePath = MediaHelper::disk('s3')->uploadFile($file, $path, $fileName = null, $withOriginalName = false);

// Delete a file from the 's3' disk
MediaHelper::disk('s3')->deleteFile($filePath);

// Upload multiple files to the 's3' disk
$uploadedFilePaths = MediaHelper::disk('s3')->uploadMultiple($files, $path, $filesNames = null, $withOriginalNames = false);

// Upload a base64 image to the 's3' disk
$uploadedImagePath = MediaHelper::disk('s3')->uploadBase64Image($encodedImage, $path, $fileName = null);

// Use the default filesystem disk (fallback to 'public' if not explicitly configured)
$uploadedFilePath = MediaHelper::uploadFile($file, $path, $fileName = null, $withOriginalName = false);

```
  
### Conclusion:
The Media Helper simplifies common file uploading and deletion tasks in your Laravel application. Its methods are designed to make managing files more efficient and user-friendly. Use the provided methods to seamlessly integrate file handling capabilities into your project.

----
