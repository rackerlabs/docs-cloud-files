
.. _delete-object:

Delete object
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    DELETE /v1/{account}/{container}/{object}

This operation permanently deletes an object from the Cloud Files storage system. (You can use ``COPY`` and then ``DELETE`` to effectively move an object.)

Perform a ``DELETE`` operation on an object to permanently remove the object from the storage system (data and metadata).

Object deletion is processed immediately at the time of the request. Any subsequent ``GET``, ``HEAD``, ``POST``, or ``DELETE`` operations return a 404 (Not Found) error unless object versioning is on and other versions exist. For more information about object versioning, see :ref:`Object versioning <object-versioning>`.

Objects with the ``X-Delete-At`` or ``X-Delete-After`` header assigned are deleted within one day of the expiration time, and the object is not served immediately after the expiration time. For more details, see :ref:`Expiring objects <expiring-objects>`.

A status code of 204 (No Content) indicates success. Status code 404 (Not Found) is returned when the object does not exist.

This operation does not require a request body and does not return a response body.

For information about bulk deletions, see :ref:`Bulk delete <bulk-delete>`.



This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|204                       |No Content               |The request succeeded.   |
+--------------------------+-------------------------+-------------------------+
|404                       |Not Found                |The requested resource   |
|                          |                         |was not found.           |
+--------------------------+-------------------------+-------------------------+


Request
""""""""""""""""


This table shows the header parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|X-Auth-Token              |String *(Required)*      |Authentication token.    |
+--------------------------+-------------------------+-------------------------+




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

+--------------------------+-------------------------+--------------------------+
|Name                      |Type                     |Description               |
+==========================+=========================+==========================+
|multipart-manifest        |String *(Optional)*      |If you include            |
|                          |                         |the                       |
|                          |                         |``multipart-manifest=get``|          
|                          |                         |query                     |
|                          |                         |parameter and the object  |
|                          |                         |is a large object, the    |
|                          |                         |object contents are not   |
|                          |                         |returned. Instead, the    |
|                          |                         |manifest is returned in   |
|                          |                         |the ``X-Object-Manifest`` |
|                          |                         |response header for       |
|                          |                         |dynamic large objects or  |
|                          |                         |in the response body for  |
|                          |                         |static large objects.     |
+--------------------------+-------------------------+--------------------------+




This operation does not accept a request body.




**Example: Delete object HTTP request**


.. code::

   DELETE /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer/MyObject HTTP/1.1
   Host: storage.clouddrive.com
   X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c





Response
""""""""""""""""


This table shows the header parameters for the response:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|Content-Length            |String *(Required)*      |The length of the        |
|                          |                         |response body that       |
|                          |                         |contains the list of     |
|                          |                         |names. If the operation  |
|                          |                         |fails, this value is the |
|                          |                         |length of the error text |
|                          |                         |in the response body.    |
+--------------------------+-------------------------+-------------------------+
|Content-Type              |String *(Required)*      |The MIME type of the     |
|                          |                         |list of names. If the    |
|                          |                         |operation fails, this    |
|                          |                         |value is the MIME type   |
|                          |                         |of the error text in the |
|                          |                         |response body.           |
+--------------------------+-------------------------+-------------------------+
|X-Trans-Id                |Uuid *(Required)*        |A unique transaction     |
|                          |                         |identifier for this      |
|                          |                         |request.                 |
+--------------------------+-------------------------+-------------------------+
|Date                      |Datetime *(Required)*    |The transaction date and |
|                          |                         |time.                    |
+--------------------------+-------------------------+-------------------------+




This operation does not return a response body.





**Example: Delete object HTTP response**


.. code::

   HTTP/1.1 204 No Content
   Content-Length: 0
   Content-Type: text/html; charset=UTF-8
   X-Trans-Id: tx36c7606fcd1843f59167c-0052d6fdac
   Date: Wed, 15 Jan 2014 21:29:16 GMT




