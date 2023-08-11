---
layout: default
title: API Response
nav_order: 2
has_children: false
permalink: api-response
---

## **API Response**

The API Response feature provides standardized response formatting and status codes.


#### **Success Response**
```json
{
  "message": "your message",
  "data": "your date"
}
```
#### **Error Response**
```json
{
  "errors": [
    {
      "status": 403,
      "title": "unauthenticated!",
      "detail": "Unauthenticated."
    }
  ]
}
```

Usage: Include the ApiResponse trait in your class, then use the provided methods such as responseSuccess, responseCreated, responseDeleted, etc., to generate appropriate responses. Refer to the documentation for a full list of available methods.

```php
$this->responseSuccess('car created successfully' , $car);
```
Available Methods

| Function                                    | Status Code          
|:--------------------------------------------|:------------------
| responseSuccess($message , $data)           | 200
| responseCreated($message,$data)             | 201 
| responseDeleted()                           | 204
| ok           | good `zoute` drop 



```php

responseSuccess($message , $data)  // returns a 200 HTTP status code
responseCreated($message,$data)  // returns a 201 HTTP status code 
  // returns an empty response with a 204 HTTP status code
responseNotFound($errorDetails,$errorTitle)  // returns a 404 HTTP status code
responseBadRequest($errorDetails,$errorTitle)  // returns a 400 HTTP status code
responseUnAuthorized($errorDetails,$errorTitle)  // returns a 403 HTTP status code
responseConflictError($errorDetails,$errorTitle)  // returns a 409 HTTP status code
responseUnprocessable($errorDetails,$errorTitle)  // returns a 422 HTTP status code
responseUnAuthenticated ($errorDetails,$errorTitle) // returns a 401 HTTP status code
responseWithCustomError($errorTitle, $errorDetails, $statusCode) //send custom error 
```


----

[^1]: [It can take up to 10 minutes for changes to your site to publish after you push the changes to GitHub](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll#creating-your-site).
