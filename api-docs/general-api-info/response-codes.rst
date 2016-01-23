.. _response-codes:

==============
Response codes
==============

Cloud Files returns an HTTP code that denotes the type of response.

The following table lists possible fault types with their associated error codes and descriptions.

+--------------------------+------------+-----------------------------------------+
|     Fault type           | Associated | Description                             |
|                          | error code |                                         |
+==========================+============+=========================================+
| OK                       | 200        | The request has succeeded. (Some API    |
|                          |            | calls might return 201 instead.)        |
+--------------------------+------------+-----------------------------------------+
| Created                  | 201        | The request has been fulfilled          |
|                          |            | and a resource was created.             |
+--------------------------+------------+-----------------------------------------+
| Accepted                 | 202        | The request has been accepted for       |
|                          |            | processing.                             |
+--------------------------+------------+-----------------------------------------+
| No Content               | 204        | The request has been fulfilled but does |
|                          |            | not return a representation (that is,   |
|                          |            | the response is empty).                 |
+--------------------------+------------+-----------------------------------------+
| Partial Content          | 206        | The request has been fulfilled the      |
|                          |            | partial GET request for the resource.   |
+--------------------------+------------+-----------------------------------------+
| Bad Request              | 400        | The request was not understood due to   |
|                          |            | bad syntax or missing required          |
|                          |            | parameters.                             |
+--------------------------+------------+-----------------------------------------+
| Unauthorized             | 401        | Authentication failed, or the user does |
|                          |            | not have permissions for a requested    |
|                          |            | operation.                              |
+--------------------------+------------+-----------------------------------------+
| Forbidden                | 403        | The server understood the request but   |
|                          |            | refused to fulfill it.                  |
+--------------------------+------------+-----------------------------------------+
| Not Found                | 404        | A requested resource was not found but  |
|                          |            | might be available again in the future. |
+--------------------------+------------+-----------------------------------------+
| Method Not Allowed       | 405        | The request method is not supported     |
|                          |            | for this resource.                      |
+--------------------------+------------+-----------------------------------------+
| Request Timeout          | 408        | The server timed out waiting for        |
|                          |            | the request.                            |
+--------------------------+------------+-----------------------------------------+
| Conflict                 | 409        | The request could not be completed due  |
|                          |            | to a conflict with the current state    |
|                          |            | of the resource.                        |
+--------------------------+------------+-----------------------------------------+
| Length Required          | 411        | The request did not specify the length  |
|                          |            | of its content, which is required       |
|                          |            | by the requested resource.              |
+--------------------------+------------+-----------------------------------------+
| Precondition Failed      | 412        | The server does not meet one of the     |
|                          |            | preconditions that the requester        |
|                          |            | put on the request.                     |
+--------------------------+------------+-----------------------------------------+
| Request Entity Too Large | 413        | The server is refusing to process a     |
|                          |            | request because the request entity is   |
|                          |            | larger than the server is willing or    |
|                          |            | able to process.                        |
+--------------------------+------------+-----------------------------------------+
| Expectation Failed       | 417        | The server cannot meet the requirements |
|                          |            | of the Expect request-header field.     |
+--------------------------+------------+-----------------------------------------+
| Unprocessable Entity     | 422        | The request could not be followed due   |
|                          |            | to semantic errors.                     |
+--------------------------+------------+-----------------------------------------+
| Too Many Requests        | 429        | Too many requests have been sent in a   |
|                          |            | given amount of time. Pause requests,   |
|                          |            | wait up to one minute, and try again.   |
|                          |            | (Intended for use with rate limiting.)  |
+--------------------------+------------+-----------------------------------------+
| Internal Server Error    | 500        | The service encountered an unexpected   |
|                          |            | condition that prevented it from        |
|                          |            | fulfilling the request.                 |
+--------------------------+------------+-----------------------------------------+
| Service Unavailable      | 503        | The service is currently unable to      |
|                          |            | handle the request due to a temporary   |
|                          |            | overloading or maintenance. This is a   |
|                          |            | temporary condition. Try again later.   |
+--------------------------+------------+-----------------------------------------+

An example of an error message follows.

**Example: Error message example**

.. code::

    HTTP/1.1 201 Created
    Last-Modified: Fri, 17 Jan 2014 17:28:35 GMT
    Content-Length: 116
    Etag: 8a964ee2a5e88be344f36c22562a6486 
    Content-Type: text/html; charset=UTF-8
    X-Trans-Id: tx4d5e4f06d357462bb732f-0052d96843 
    Date: Fri, 17 Jan 2014 17:28:35 GMT

