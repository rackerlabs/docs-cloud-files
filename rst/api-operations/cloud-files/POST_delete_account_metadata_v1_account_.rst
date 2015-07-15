=============================================================================
Delete Account Metadata -  Rackspace Cloud Files™ Developer Guide
=============================================================================

Delete Account Metadata
~~~~~~~~~~~~~~~~~~~~~~~~~

`Request <POST_delete_account_metadata_v1_account_.rst#request>`__
`Response <POST_delete_account_metadata_v1_account_.rst#response>`__

.. code-block:: javascript

    POST /v1/{account}

Deletes account metadata.

To delete a metadata header, use the ``POST`` operation to send an empty value for that particular header.

If the tool that you use to communicate with Cloud Files does not support empty headers, such as an older version of cURL, send the ``X-Remove-Account-Meta-name: arbitrary value`` header. The ``arbitrary value`` is ignored. In the following example request, ``X-Remove-Account-Meta-Book: x`` is used.

A status code of 200 through 299 indicates success.

This operation does not require a request body and does not return a response body.



This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|204                       |No Content               |The request succeeded.   |
|                          |                         |The server fulfilled the |
|                          |                         |request but does not     |
|                          |                         |need to return a body.If |
|                          |                         |the operation succeeds,  |
|                          |                         |this value is zero       |
|                          |                         |(0).If the operation     |
|                          |                         |fails, this value is the |
|                          |                         |length of theerror text  |
|                          |                         |in the response body.If  |
|                          |                         |the operation fails,     |
|                          |                         |this value is the MIME   |
|                          |                         |typeof the error text in |
|                          |                         |the response body.A      |
|                          |                         |unique transaction       |
|                          |                         |identifier for this      |
|                          |                         |request.The transaction  |
|                          |                         |date and time.           |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad Request              |The request could not be |
|                          |                         |understood by the server |
|                          |                         |due to malformed syntax. |
+--------------------------+-------------------------+-------------------------+


Request
^^^^^^^^^^^^^^^^^

This table shows the URI parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|{account}                 |xsd:string               |Yourunique account       |
|                          |                         |identifier.              |
+--------------------------+-------------------------+-------------------------+








**Example Delete account metadata: HTTP request**


.. code::

    POST /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123 HTTP/1.1
    Host: storage.clouddrive.com
    X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c
    X-Remove-Account-Meta-Book: x


Response
^^^^^^^^^^^^^^^^^^





**Example Delete account metadata: HTTP response**


.. code::

    HTTP/1.1 204 No Content
    Content-Length: 0
    Content-Type: text/html; charset=UTF-8
    X-Trans-Id: txe749a717ee5e4da7a6895-0052cf2286dfw1
    Date: Thu, 09 Jan 2014 22:28:22 GMT

