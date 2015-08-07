
.. THIS OUTPUT IS GENERATED FROM THE WADL. DO NOT EDIT.

Delete object
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    DELETE /v1/{account}/{container}/{object}

Permanently deletes an object from the Cloud Files storage system. (You can use ``COPY`` and then ``DELETE`` to effectively move an object.)

Perform a ``DELETE`` operation on an object to permanently remove the object from the storage system (data and metadata).

Object deletion is processed immediately at the time of the request. Any subsequent ``GET``, ``HEAD``, ``POST``, or ``DELETE`` operations return a 404 (Not Found) error unless object versioning is on and other versions exist. For more information about object versioning, see `Object versioning <http://docs.rackspace.com/files/api/v1/cf-devguide/content/Object_Versioning-e1e3230.html>`__.

Objects with the ``X-Delete-At`` or ``X-Delete-After`` header assigned are deleted within one day of the expiration time, and the object is not served immediately after the expiration time. For more details, see `Expiring objects <http://docs.rackspace.com/files/api/v1/cf-devguide/content/Expiring_Objects-e1e3228.html>`__.

A status code of 204 (No Content) indicates success. Status code 404 (Not Found) is returned when the object does not exist.

This operation does not require a request body and does not return a response body.

For information about bulk deletions, see `Bulk delete <http://docs.rackspace.com/files/api/v1/cf-devguide/content/Bulk_Delete-d1e2338.html.html>`__.



This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|204                       |No Content               |The request succeeded.   |
|                          |                         |The server fulfilled the |
|                          |                         |request but does not     |
|                          |                         |need to return a body.   |
+--------------------------+-------------------------+-------------------------+
|404                       |Not Found                |The requested resource   |
|                          |                         |was not found.           |
+--------------------------+-------------------------+-------------------------+


Request
""""""""""""""""

This table shows the URI parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|{account}                 |String                   |Your unique account      |
|                          |                         |identifier.              |
+--------------------------+-------------------------+-------------------------+
|{container}               |String                   |The unique identifier of |
|                          |                         |the container.           |
+--------------------------+-------------------------+-------------------------+
|{object}                  |String                   |The unique identifier of |
|                          |                         |the object.              |
+--------------------------+-------------------------+-------------------------+



This table shows the query parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|multipart-manifest        |String *(Optional)*      |If you include           |
|                          |                         |the``multipart-          |
|                          |                         |manifest=get`` query     |
|                          |                         |parameter and the object |
|                          |                         |is a large object, the   |
|                          |                         |object contents are not  |
|                          |                         |returned. Instead, the   |
|                          |                         |manifest is returned in  |
|                          |                         |the``X-Object-Manifest`` |
|                          |                         |response header for      |
|                          |                         |dynamic large objects or |
|                          |                         |in the response body for |
|                          |                         |static large objects.    |
+--------------------------+-------------------------+-------------------------+




This operation does not accept a request body.




**Example Delete object: HTTP request**


.. code::

    DELETE /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer/MyObject HTTP/1.1
    Host: storage.clouddrive.com
    X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c


Response
""""""""""""""""





**Example Delete object: HTTP response**


.. code::

    HTTP/1.1 204 No Content
    Content-Length: 0
    Content-Type: text/html; charset=UTF-8
    X-Trans-Id: tx36c7606fcd1843f59167c-0052d6fdac
    Date: Wed, 15 Jan 2014 21:29:16 GMT


