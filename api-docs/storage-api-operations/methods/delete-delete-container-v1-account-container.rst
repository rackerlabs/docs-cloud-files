.. _delete-container:

Delete container
^^^^^^^^^^^^^^^^

.. code::

    DELETE /v1/{account}/{container}

This operation deletes an empty container.

A ``DELETE`` operation against a storage container permanently removes it. The
container must be empty before it can be deleted.

Before using ``DELETE``, you can use a ``GET`` operation against the container
to list any objects that it contains. (See :ref:`Show container details and
list objects <get-container-details-and-list-objects>`.)

A status code of 204 (No Content) indicates success. A status code of 404
(Not Found) is returned if the requested container is not found. A status code
of 409 (Conflict) is returned if the container is not empty.

This table shows the possible response codes for this operation:

+--------------------------+-------------------------+------------------------+
|Response Code             |Name                     |Description             |
+==========================+=========================+========================+
|204                       |No Content               |The request succeeded.  |
+--------------------------+-------------------------+------------------------+
|404                       |Not Found                |The requested resource  |
|                          |                         |was not found.          |
+--------------------------+-------------------------+------------------------+
|409                       |Conflict                 |The request could not be|
|                          |                         |completed due to a      |
|                          |                         |conflict with the       |
|                          |                         |current state of the    |
|                          |                         |resource.               |
+--------------------------+-------------------------+------------------------+

Request
"""""""

This table shows the URI parameters for the request:

+--------------------------+-------------------------+------------------------+
|Name                      |Type                     |Description             |
+==========================+=========================+========================+
|{account}                 |String                   |Your unique account     |
|                          |                         |identifier.             |
+--------------------------+-------------------------+------------------------+
|{container}               |String                   |The unique identifier of|
|                          |                         |the container.          |
+--------------------------+-------------------------+------------------------+

This table shows the header parameters for the request:

+--------------------------+-------------------------+------------------------+
|Name                      |Type                     |Description             |
+==========================+=========================+========================+
|X-Auth-Token              |String *(Required)*      |Authentication token.   |
+--------------------------+-------------------------+------------------------+

This operation does not accept a request body.

**Example: Delete container HTTP request**

.. code::

   DELETE /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer HTTP/1.1
   Host: storage.clouddrive.com
   X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c

Response
""""""""

This table shows the header parameters for the response:

+--------------------------+-------------------------+------------------------+
|Name                      |Type                     |Description             |
+==========================+=========================+========================+
|Content-Length            |String                   |The length of the       |
|                          |                         |response body that      |
|                          |                         |contains the list of    |
|                          |                         |names. If the operation |
|                          |                         |fails, this value is the|
|                          |                         |length of the error text|
|                          |                         |in the response body.   |
+--------------------------+-------------------------+------------------------+
|Content-Type              |String                   |The MIME type of the    |
|                          |                         |list of names. If the   |
|                          |                         |operation fails, this   |
|                          |                         |value is the MIME type  |
|                          |                         |of the error text in the|
|                          |                         |response body.          |
+--------------------------+-------------------------+------------------------+
|X-Trans-Id                |Uuid                     |A unique transaction    |
|                          |                         |identifier for this     |
|                          |                         |request.                |
+--------------------------+-------------------------+------------------------+
|Date                      |Datetime                 |The transaction date and|
|                          |                         |time.                   |
+--------------------------+-------------------------+------------------------+

This operation does not return a response body.

**Example: Delete container HTTP response**

.. code::

   HTTP/1.1 204 No Content
   Content-Length: 0
   Content-Type: text/html; charset=UTF-8
   X-Trans-Id: txf76c375ebece4df19c84c-0052d81f14
   Date: Thu, 16 Jan 2014 18:04:04 GMT
