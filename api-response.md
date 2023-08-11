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
| responseSuccess($message , $data)                                | 200
| responseCreated($message,$data)                                  | 201 
| responseDeleted()                                                | 204
|responseNotFound($errorDetails,$errorTitle)                       | 404
|responseBadRequest($errorDetails,$errorTitle)                     | 400
|responseUnAuthorized($errorDetails,$errorTitle)                   | 403
|responseConflictError($errorDetails,$errorTitle)                  | 409
|responseUnprocessable($errorDetails,$errorTitle)                  | 422
|responseUnAuthenticated($errorDetails,$errorTitle)                | 401
|responseWithCustomError($errorTitle, $errorDetails, $statusCode)  | -

----
