
.. _list-metadata-for-cdn-enabled-container:

List metadata for CDN-enabled container
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    HEAD /v1/{account}/{container}

This operation gets a CDN-enabled container's metadata.

You can view CDN-enabled container details by performing a ``HEAD`` operation on a container where the ``Host`` header value is one of the ``cdnCloudFiles`` service access endpoints. (For the CDN endpoints, see :ref:`Service access endpoints <service-access>`.)

.. note::
   Remember that your ``HEAD`` operation must be on the CDN host (for example, ``cdn.clouddrive.com`` ). Otherwise, you will see the metadata for your private container as described in :ref:`Get account metadata <get-account-metadata>`.
   
   

A 204 (No Content) HTTP status code is returned if the account has no containers. Otherwise, the status code of 200 (OK) is returned. Status code 404 (Not Found) is returned if the requested container was not found.



This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |OK                       |The request has          |
|                          |                         |succeeded.               |                
+--------------------------+-------------------------+-------------------------+
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
|{account}                 |String *(Required)*      |Your unique account      |
|                          |                         |identifier.              |
+--------------------------+-------------------------+-------------------------+
|{container}               |String *(Required)*      |The unique identifier of |
|                          |                         |the container.           |
+--------------------------+-------------------------+-------------------------+





This operation does not accept a request body.




**Example: List metadata for CDN-enabled container HTTP request**


.. code::

   HEAD /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer HTTP/1.1
   Host: cdn.clouddrive.com
   X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c
   





Response
""""""""""""""""


This table shows the header parameters for the response:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|X-Cdn-Uri                 |String *(Required)*      |The URI for downloading  |
|                          |                         |the object over HTTP.    |
|                          |                         |This URI can be combined |
|                          |                         |with any object name     |
|                          |                         |within the container to  |
|                          |                         |form the publicly        |
|                          |                         |accessible URI for that  |
|                          |                         |object for distribution  |
|                          |                         |over a CDN system.       |
+--------------------------+-------------------------+-------------------------+
|X-Ttl                     |Int *(Required)*         |The TTL value in         |
|                          |                         |seconds. The default     |
|                          |                         |value is 259200 seconds, |
|                          |                         |or 72 hours. The minimum |
|                          |                         |TTL is 15 minutes (or    |
|                          |                         |900 seconds), and the    |
|                          |                         |maximum is 1 year        |
|                          |                         |(31536000 seconds).      |
+--------------------------+-------------------------+-------------------------+
|X-Cdn-Enabled             |Boolean *(Required)*     |True or False to         |
|                          |                         |indicate whether the     |
|                          |                         |container is currently   |
|                          |                         |marked to allow public   |
|                          |                         |serving of objects       |
|                          |                         |through the CDN.         |
+--------------------------+-------------------------+-------------------------+
|X-Log-Retention           |Boolean *(Required)*     |True or False to         |
|                          |                         |indicate whether the CDN |
|                          |                         |access logs should be    |
|                          |                         |collected and stored in  |
|                          |                         |the Cloud Files storage  |
|                          |                         |system.                  |
+--------------------------+-------------------------+-------------------------+
|X-Cdn-Ssl-Uri             |String *(Required)*      |The URI for downloading  |
|                          |                         |the object over HTTPS,   |
|                          |                         |using SSL. (The user     |
|                          |                         |cannot have custom SSL   |
|                          |                         |certificates because the |
|                          |                         |Rackspace CDN partner    |
|                          |                         |does not provide that    |
|                          |                         |feature.                 |
+--------------------------+-------------------------+-------------------------+
|X-Cdn-Streaming-Uri       |String *(Required)*      |The URI for video        |
|                          |                         |streaming that uses HTTP |
|                          |                         |Dynamic Streaming from   |
|                          |                         |Adobe.                   |
+--------------------------+-------------------------+-------------------------+
|X-Cdn-Ios-Uri             |String *(Required)*      |The URI for video        |
|                          |                         |streaming that uses HTTP |
|                          |                         |Live Streaming from      |
|                          |                         |Apple.                   |
+--------------------------+-------------------------+-------------------------+




This operation does not return a response body.





**Example: Get CDN-enabled container metadata HTTP response**


.. code::

   HTTP/1.1 204 No Content
   X-Cdn-Ssl-Uri: https://
    83c49b9a2f7ad18250b3-346eb45fd42c58ca13011d659bfc1ac1.
    ssl.cf0.rackcdn.com
   X-Ttl: 259200
   X-Cdn-Uri: http://081e40d3ee1cec5f77bf-346eb45fd42c58ca13011d659bfc1ac1.
    r49.cf0.rackcdn.com
   X-Cdn-Enabled: True
   X-Log-Retention: False
   X-Cdn-Streaming-Uri: http://084cc2790632ccee0a12-346eb45fd42c58ca13011d
    659bfc1ac1.r49.stream.cf0.rackcdn.com
   X-Trans-Id: tx82a6752e00424edb9c46fa2573132e2c
   Content-Length: 0




