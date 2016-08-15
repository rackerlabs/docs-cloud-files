.. _bulk-delete:

===========
Bulk delete
===========

You can delete multiple objects or containers from an account by using a
single bulk delete request, which is a **DELETE** request with the
``?bulk-delete set`` query parameter. The ``Content-Type``
header of the request, if set, must be set to ``text/plain``. You direct
the request to the root of the service endpoints. The
body of the **DELETE** request is a newline-separated list of
URL-encoded objects to delete. You can delete 10,000 objects per
request.

.. note:: This bulk operation involves middleware that conducts many operations
   on a single request.

The objects specified in the **DELETE** request body must be URL-encoded
and in the following form:

``/containerName/objectName``

Containers (which must be empty at time of delete) have the following
form:

``/containerName``

Create a text file similar to the following example,
objects\_to\_delete.txt, with the names of the objects that you want to
delete.

**Example: Create text file for bulk delete request**

.. code::

    $ cat objects_to_delete.txt
    /containerName/objectName1
    /containerName/objectName2
    /containerName/objectName3
    /containerName/objectName4

You can use a cURL request similar to the following example for the bulk
delete.

**Example: cURL request for the bulk delete**

.. code::

    $ curl -i -XDELETE -H'x-auth-token: f064c46a782c444cb4ba4b6434288f7c' https://storage101.dfw1.clouddrive.com/v1/MossoCloudFS_000000\?bulk-delete -T ./objects_to_delete.txt

An HTTP request for the bulk delete is similar to the following example.

**Example: HTTP request for the bulk delete**

.. code::

    DELETE /v1/MossoCloudFS_000000?bulk-delete HTTP/1.1
    Host: storage101.dfw1.clouddrive.com
    x-auth-token:f064c46a782c444cb4ba4b6434288f7c
    Content-Length: 108

    /containerName/objectName1
    /containerName/objectName2
    /containerName/objectName3
    /containerName/objectName4

The response is similar to the extract archive responses in that every
response is 200 OK and the response body must be parsed for actual
results. The following example shows the response body, formatted in
JSON, from a successful request.

**Example: Successful bulk delete response**

.. code::

    HTTP/1.1 100 Continue

    HTTP/1.1 200 OK
    Content-Type: application/json; charset=UTF-8
    X-Trans-Id: tx52fe4601dde24e2b8e7cb-0051912ca8
    Date: Thu, 23 Oct 2014 15:16:41 GMT
    Transfer-Encoding: chunked

    {
      "Number Not Found": 0,
      "Response Status": "200 OK",
      "Errors": [],
      "Number Deleted": 4,
      "Response Body": ""
    }

The following example shows a response with errors.

**Example: Bulk delete response with errors**

.. code::

    HTTP/1.1 100 Continue

    HTTP/1.1 200 OK
    Content-Type: application/json; charset=UTF-8
    X-Trans-Id: tx28552a8cd9cb441dad3ad-0051912d2d
    Date: Mon, 13 May 2013 18:13:01 GMT
    Transfer-Encoding: chunked

    {
      "Number Not Found": 0,
      "Response Status": "400 Bad Request",
      "Errors": [
        [
          "/v1/AUTH_test/non_empty_container",
          "409 Conflict"
        ]
      ],
      "Number Deleted": 0,
      "Response Body": ""
    }

The list of errors is a list of tuples in the form
``[objectPath, errorResponse]``. The ``objectPath`` is the
full path of where the object (or container) was to be deleted. The
``errorResponse`` is the HTTP status of the response for that individual
**DELETE** request.

If all items were successfully deleted (or did not exist), the
``Response Status`` is 200 OK. If any items failed to delete,
the ``Response Status`` code corresponds to the subrequest's error.
Possible codes are 400, 401, and 502. In all cases, the
``Response Body`` specifies the number of items successfully deleted or
not found as well as a list of those that failed. The return body is
formatted in the way specified in the request's ``Accept`` header.
Acceptable formats are ``text/plain``, ``application/json``,
``application/xml``, and ``text/xml``.
