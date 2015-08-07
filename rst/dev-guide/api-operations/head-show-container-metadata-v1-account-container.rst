
.. THIS OUTPUT IS GENERATED FROM THE WADL. DO NOT EDIT.

Show container metadata
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    HEAD /v1/{account}/{container}

Shows container metadata, including the number of objects in the container and the total bytes for all objects stored in the container.

Use a ``HEAD`` operation against the container to return the following metadata: 



*  How many objects are in the container ( ``X-Container-Object-Count`` )
*  The total bytes for all objects stored in the container ( ``X-Container-Bytes-Used`` )
*  Any custom metadata that is set on the container ( ``X-Container-Meta-name`` )


To set and edit your custom metadata, see `Create or update container metadata <http://docs.rackspace.com/files/api/v1/cf-devguide/content/POST_updateacontainermeta_v1__account___container__containerServicesOperations_d1e000.html>`__.

If the container exists, a status code of 200 through 299 is returned. If the container does not exist, a status code of 404 (Not Found) is returned.

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





This operation does not accept a request body.




**Example Get container metadata: HTTP request**


.. code::

    HEAD /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer HTTP/1.1
    Host: storage.clouddrive.com
    X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c
    


Response
""""""""""""""""





**Example Get container metadata: HTTP response**


.. code::

    HTTP/1.1 204 No Content
    Content-Length: 0
    X-Container-Object-Count: 1
    Accept-Ranges: bytes
    X-Container-Meta-Book: TomSawyer
    X-Timestamp: 1389727543.65372
    X-Container-Meta-Author: SamuelClemens
    X-Container-Bytes-Used: 14
    Content-Type: text/plain; charset=utf-8
    X-Trans-Id: tx0287b982a268461b9ec14-0052d826e2
    Date: Thu, 16 Jan 2014 18:37:22 GMT


