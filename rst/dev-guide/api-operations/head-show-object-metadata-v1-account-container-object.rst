
.. THIS OUTPUT IS GENERATED FROM THE WADL. DO NOT EDIT.

Show object metadata
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    HEAD /v1/{account}/{container}/{object}

Shows object metadata.

Perform a HEAD operation on an object to retrieve object metadata and other standard HTTP headers.

This operation does not return a response body. Metadata is returned as HTTP headers.

.. note::
   JIRA ticket 1-/ 21 metadata / response clarity -- dsh 2012-03-07 The ``HEAD`` return code for an object is different than the ``HEAD`` return code for a container. A ``HEAD`` request does not return a message body in the response, so a status code of 200 through 299 indicates success. When a ``HEAD`` request is performed against a container, it queries the container databases, and it does not retrieve the content from them. Thus, this operation returns the 204 (No Content) status code. However, when a ``HEAD`` request is performed against an object, it returns a 200 OK status code because it can view the content. 
   
   



This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |OK                       |The request has          |
|                          |                         |succeeded. The           |
|                          |                         |information returned     |
|                          |                         |with the response is     |
|                          |                         |dependent on the method  |
|                          |                         |used in the request.     |
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

+----------------+----------------+--------------------------------------------+
|Name            |Type            |Description                                 |
+================+================+============================================+
|signature       |String          |Used with temporary URLs to sign the        |
|                |*(Optional)*    |request. For more information about         |
|                |                |temporary URLs, see `TempURL                |
|                |                |<http://docs.rackspace.com/files/api/v1/cf- |
|                |                |devguide/content/TempURL-d1a4450.html>`__.  |
+----------------+----------------+--------------------------------------------+
|expires         |String          |Used with temporary URLs to specify the     |
|                |*(Optional)*    |expiry time of the signature. For more      |
|                |                |information about temporary URLs, see       |
|                |                |`TempURL                                    |
|                |                |<http://docs.rackspace.com/files/api/v1/cf- |
|                |                |devguide/content/TempURL-d1a4450.html>`__.  |
+----------------+----------------+--------------------------------------------+




This operation does not accept a request body.




**Example Get object metadata: HTTP request**


.. code::

    HEAD /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer/MyObject HTTP/1.1
    Host: storage.clouddrive.com
    X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c


Response
""""""""""""""""





**Example Get object metadata: HTTP response**


.. code::

    HTTP/1.1 200 OK
    Date: Thu, 10 Jun 2010 20:59:39 GMT
    Last-Modified: Fri, 11 Jun 2010 13:40:18 GMT
    ETag: 8a964ee2a5e88be344f36c22562a6486
    Content-Length: 512000
    Content-Type: text/plain; charset=UTF-8
    X-Object-Meta-Meat: Bacon
    X-Object-Meta-Fruit: Apple
    X-Object-Meta-Veggie: Beans
    X-Object-Meta-Dairy: Cheese


