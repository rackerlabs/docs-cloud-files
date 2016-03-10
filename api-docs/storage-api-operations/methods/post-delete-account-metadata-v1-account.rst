
.. _delete-account-metadata:

Delete account metadata
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    POST /v1/{account}

This operation deletes account metadata.

To delete a metadata header, use the ``POST`` operation to send an empty value for that particular header.

If the tool that you use to communicate with Cloud Files does not support empty headers, such as an older version of cURL, send the ``X-Remove-Account-Meta-name: arbitrary value`` header. The ``arbitrary value`` is ignored. In the following example request, ``X-Remove-Account-Meta-Book: x`` is used.

A status code of 200 through 299 indicates success.



This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|204                       |No Content               |The request succeeded.   |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad Request              |The request could not be |
|                          |                         |understood by the server |
|                          |                         |due to malformed syntax. |
+--------------------------+-------------------------+-------------------------+


Request
""""""""""""""""


This table shows the header parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|X-Auth-Token              |String *(Required)*      |Authentication token.    |
+--------------------------+-------------------------+-------------------------+
|X-Account-Meta-Temp-URL-  |String *(Optional)*      |The secret key value for |
|Key                       |                         |temporary URLs.          |
+--------------------------+-------------------------+-------------------------+
|X-Account-Meta-Temp-URL-  |String *(Optional)*      |A second secret key      |
|Key-2                     |                         |value for temporary      |
|                          |                         |URLs. The second key     |
|                          |                         |enables you to rotate    |
|                          |                         |keys by having an old    |
|                          |                         |and new key active at    |
|                          |                         |the same time.           |
+--------------------------+-------------------------+-------------------------+
|X-Remove-Account-Meta-name|String *(Required)*      |Header to send to delete |
|                          |                         |account metadata.        |
|                          |                         |Replace ``name`` at the  |
|                          |                         |end of the header with   |
|                          |                         |the name for your        |
|                          |                         |metadata.                |
+--------------------------+-------------------------+-------------------------+




This table shows the URI parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|{account}                 |String                   |Your unique account      |
|                          |                         |identifier.              |
+--------------------------+-------------------------+-------------------------+





This operation does not accept a request body.




**Example: Delete account metadata HTTP request**


.. code::

   POST /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123 HTTP/1.1
   Host: storage.clouddrive.com
   X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c
   X-Remove-Account-Meta-Book: x





Response
""""""""""""""""


This table shows the header parameters for the response:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|Content-Length            |String *(Required)*      |If the operation         |
|                          |                         |succeeds, this value is  |
|                          |                         |zero (0). If the         |
|                          |                         |operation fails, this    |
|                          |                         |value is the length of   |
|                          |                         |the error text in the    |
|                          |                         |response body.           |
+--------------------------+-------------------------+-------------------------+
|Content-Type              |String *(Required)*      |If the operation fails,  |
|                          |                         |this value is the MIME   |
|                          |                         |type of the error text   |
|                          |                         |in the response body.    |
+--------------------------+-------------------------+-------------------------+
|X-Trans-Id                |Uuid *(Required)*        |A unique transaction     |
|                          |                         |identifier for this      |
|                          |                         |request.                 |
+--------------------------+-------------------------+-------------------------+
|Date                      |Datetime *(Required)*    |The transaction date and |
|                          |                         |time.                    |
+--------------------------+-------------------------+-------------------------+




This operation does not return a response body.




**Example: Delete account metadata HTTP response**


.. code::

   HTTP/1.1 204 No Content
   Content-Length: 0
   Content-Type: text/html; charset=UTF-8
   X-Trans-Id: txe749a717ee5e4da7a6895-0052cf2286dfw1
   Date: Thu, 09 Jan 2014 22:28:22 GMT




