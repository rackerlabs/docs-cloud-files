
.. THIS OUTPUT IS GENERATED FROM THE WADL. DO NOT EDIT.

Get account metadata
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    HEAD /v1/{account}

Gets account metadata.

Perform a ``HEAD`` operation on your storage account URL to get the following information: 



*  The number of containers that you have in your account ( ``X-Account-Container-Count`` )
*  The number of objects that are stored in the containers in your account ( ``X-Account-Object-Count`` )
*  The total bytes that are stored for your account ( ``X-Account-Bytes-Used`` )


An HTTP status code of 200 through 299 indicates success. In the example, a 204 (No Content) status code is returned. A 401 (Unauthorized) status code is returned for an invalid account or authentication token. 

This operation does not require a request body and does not return a response body.



This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|204                       |No Content               |The request succeeded.   |
|                          |                         |The server fulfilled the |
|                          |                         |request but does not     |
|                          |                         |need to return a body.   |
+--------------------------+-------------------------+-------------------------+
|401                       |Unauthorized             |Authentication has       |
|                          |                         |failed.                  |
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





This operation does not accept a request body.




**Example Get account metadata: HTTP request**


.. code::

    HEAD /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123 HTTP/1.1
    Host: storage.clouddrive.com
    X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c


Response
""""""""""""""""





**Example Get account metadata: HTTP response**


.. code::

    HTTP/1.1 204 No Content
    Content-Length: 0
    X-Account-Object-Count: 573
    X-Timestamp: 1369081921.78518
    X-Account-Meta-Temp-Url-Key: ed6a04a9f70458575112811a9af5284e
    X-Account-Bytes-Used: 14268918
    X-Account-Container-Count: 1
    Content-Type: text/plain; charset=utf-8
    Accept-Ranges: bytes
    X-Trans-Id: tx8e82a77399724e40a90e8-0052cf0e52dfw1
    Date: Thu, 09 Jan 2014 21:02:10 GMT


