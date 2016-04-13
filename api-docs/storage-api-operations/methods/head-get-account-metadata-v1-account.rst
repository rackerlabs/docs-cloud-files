
.. _get-account-metadata:

Get account metadata
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    HEAD /v1/{account}


This operation performs a ``HEAD`` operation on your storage account URL to get the following information: 



*  The number of containers that you have in your account ( ``X-Account-Container-Count`` )
*  The number of objects that are stored in the containers in your account ( ``X-Account-Object-Count`` )
*  The total bytes that are stored for your account ( ``X-Account-Bytes-Used`` )


An HTTP status code of 200 through 299 indicates success. In the example, a 204 (No Content) status code is returned. A 401 (Unauthorized) status code is returned for an invalid account or authentication token. 


This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|204                       |No Content               |The request succeeded.   |
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



This table shows the header parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|X-Auth-Token              |String *(Required)*      |Authentication token.    |
+--------------------------+-------------------------+-------------------------+








This operation does not accept a request body.




**Example: Get account metadata HTTP request**


.. code::

   HEAD /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123 HTTP/1.1
   Host: storage.clouddrive.com
   X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c





Response
""""""""""""""""


This table shows the header parameters for the response:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|X-Account-Object-Count    |Int                      |The total number of      |
|                          |                         |objects that are stored  |
|                          |                         |in Cloud Files for the   |
|                          |                         |account.                 |
+--------------------------+-------------------------+-------------------------+
|X-Account-Bytes-Used      |Int                      |The total number of      |
|                          |                         |bytes that are stored in |
|                          |                         |Cloud Files for the      |
|                          |                         |account.                 |
+--------------------------+-------------------------+-------------------------+
|X-Account-Container-Count |Int                      |The total number of      |
|                          |                         |containers that are      |
|                          |                         |stored in the Cloud      |
|                          |                         |Files for the account.   |
+--------------------------+-------------------------+-------------------------+
|Content-Length            |String                   |If the operation         |
|                          |                         |succeeds, this value is  |
|                          |                         |zero (0). If the         |
|                          |                         |operation fails, this    |
|                          |                         |value is the length of   |
|                          |                         |the error text in the    |
|                          |                         |response body.           |
+--------------------------+-------------------------+-------------------------+
|Content-Type              |String                   |If the operation fails,  |
|                          |                         |this value is the MIME   |
|                          |                         |type of the error text   |
|                          |                         |in the response body.    |
+--------------------------+-------------------------+-------------------------+
|X-Trans-Id                |Uuid                     |A unique transaction     |
|                          |                         |identifier for this      |
|                          |                         |request.                 |
+--------------------------+-------------------------+-------------------------+
|Date                      |Datetime                 |The transaction date and |
|                          |                         |time.                    |
+--------------------------+-------------------------+-------------------------+
|Accept-Ranges             |String                   |The type of ranges       |
|                          |                         |accepted.                |
+--------------------------+-------------------------+-------------------------+
|X-Account-Meta-name       |String                   |The custom account       |
|                          |                         |metadata item,           |
|                          |                         |where ``name`` is the    |
|                          |                         |name of the metadata     |
|                          |                         |item. One ``X-Account-   |
|                          |                         |Meta-name`` response     |
|                          |                         |header appears for each  |
|                          |                         |metadata item (for       |
|                          |                         |each ``name``).          |
+--------------------------+-------------------------+-------------------------+
|X-Account-Meta-Temp-URL-  |String                   |The secret key value for |
|Key                       |                         |temporary URLs. If not   |
|                          |                         |set, this header is not  |
|                          |                         |returned by this         |
|                          |                         |operation.               |
+--------------------------+-------------------------+-------------------------+
|X-Account-Meta-Temp-URL-  |String                   |A second secret key      |
|Key-2                     |                         |value for temporary      |
|                          |                         |URLs. If not set, this   |
|                          |                         |header is not returned   |
|                          |                         |by this operation.       |
+--------------------------+-------------------------+-------------------------+










**Example: Get account metadata HTTP response**


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




