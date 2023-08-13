---
layout: default
title: API Response
nav_order: 2
has_children: false
permalink: api-response
---

## **API Response**

The API Response feature streamlines the process of generating consistent and standardized JSON responses in your API. It provides a set of methods for creating both successful and error responses, ensuring clarity and coherence in your API interactions.
### Usage :
### Including the ApiResponse Trait
To take advantage of the API Response functionality, include the `ApiResponse` trait in your class:
```php
use Essa\APIToolKit\Api\ApiResponse;

class YourController extends Controller
{
    use ApiResponse;

    // Your methods here
}
```
### Success Response
The `responseSuccess` method generates a successful JSON response with a specified message and data:
```php
$car = // Your car data here

return $this->responseSuccess('Car created successfully', $car);
```
The response structure will be:

```json
{
    "message": "Car created successfully",
    "data": // Your car data here
}
```
### Error Response
The APIError method constructs an error response with a given status code, title, and optional details. You can use other provided error response methods like `responseNotFound`, `responseUnAuthorized`, and more to generate specific error responses.
```php
$errorDetails = 'Unauthenticated.';
return $this->responseUnAuthenticated($errorDetails, 'Unauthorized');
```
The error response structure will be:
```json
{
    "errors": [
        {
            "status": 401,
            "title": "Unauthorized",
            "detail": "Unauthenticated."
        }
    ]
}
```
### Available Methods
Here is a list of available methods for generating standardized responses:


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

### Conclusion:
The API Response feature simplifies the process of generating standardized responses in your API. By including the `ApiResponse` trait and utilizing the provided methods, you can ensure consistent and clear interactions between your API and clients, enhancing the user experience and overall code maintainability.


----
