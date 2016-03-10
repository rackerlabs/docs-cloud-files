
.. _update-cdn-enabled-container-metadata:

Update CDN-enabled container metadata
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    POST /v1/{account}/{container}

This operation updates the CDN-enabled container's metadata.

A ``POST`` operation against a CDN-enabled container adjusts the following metadata:



* ``X-Log-Retention``
* ``X-Cdn-Enabled``
* ``X-Ttl``




A status code of 204 (No Content) indicates success. Status code 404 (Not Found) is returned if the requested container is not found.

This operation does not require a request body and does not return a response body.



This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|204                       |No Content               |The server fulfilled the |
|                          |                         |request but does not     |
|                          |                         |need to return a body.   |
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
|X-Log-Retention           |Boolean *(Optional)*     |``True`` or ``False`` to |
|                          |                         |indicate whether the CDN |
|                          |                         |access logs should be    |
|                          |                         |collected and stored in  |
|                          |                         |the Cloud Files storage  |
|                          |                         |system.                  |
+--------------------------+-------------------------+-------------------------+
|X-Cdn-Enabled             |Boolean *(Optional)*     |``True`` or ``False`` to |
|                          |                         |enable or disable public |
|                          |                         |sharing over the CDN. If |
|                          |                         |you have content         |
|                          |                         |currently cached in the  |
|                          |                         |CDN, setting your        |
|                          |                         |container back to        |
|                          |                         |private does not purge   |
|                          |                         |the CDN cache. You have  |
|                          |                         |to wait for the TTL to   |
|                          |                         |expire or purge the      |
|                          |                         |objects.                 |
+--------------------------+-------------------------+-------------------------+
|X-Ttl                     |Int *(Optional)*         |The TTL value in         |
|                          |                         |seconds. The default     |
|                          |                         |value is 259200 seconds, |
|                          |                         |or 72 hours. The minimum |
|                          |                         |TTL is 15 minutes (or    |
|                          |                         |900 seconds), and the    |
|                          |                         |maximum is 1 year        |
|                          |                         |(31536000 seconds).      |
+--------------------------+-------------------------+-------------------------+




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




**Example: Update CDN-enabled container metadata HTTP request**


.. code::

   POST /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer HTTP/1.1
   Host: cdn.clouddrive.com
   X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c
   X-Ttl: 86400
   X-Cdn-Enabled: True
   X-Log-Retention: True





Response
""""""""""""""""




This operation does not return a response body.





**Example: Update CDN-enabled container metadata HTTP response**


.. code::

   HTTP/1.1 204 No Content
   X-Cdn-Ssl-Uri: https://83c49b9a2f7ad18250b3-346eb45fd42c58ca13011d659bfc1ac1.ssl.cf0.rackcdn.com
   X-Ttl: 259200
   X-Cdn-Uri: http://081e40d3ee1cec5f77bf-346eb45fd42c58ca13011d659bfc1ac1.r49.cf0.rackcdn.com
   X-Cdn-Enabled: True
   X-Log-Retention: False
   X-Cdn-Streaming-Uri: http://084cc2790632ccee0a12-346eb45fd42c58ca13011d659bfc1ac1.r49.stream.cf0.rackcdn.com
   X-Trans-Id: tx82a6752e00424edb9c46fa2573132e2c
   Content-Length: 0




