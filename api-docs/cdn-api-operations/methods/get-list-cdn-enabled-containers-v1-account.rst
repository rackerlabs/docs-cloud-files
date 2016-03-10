
.. _list-cdn-enabled-containers:

List CDN-enabled containers
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /v1/{account}

This operation lists CDN-enabled containers sorted by name.

``GET`` operations against the ``cloudFilesCDN`` endpoints for an account retrieve a list of CDN-enabled containers. No private containers appear in the list. (For the CDN endpoints, see :ref:`Service access endpoints <service-access>`.)

A list of CDN-enabled containers is returned in the response body, one container name per line.

An HTTP response status code of 200 through 299 indicates success. A 200 (OK) code is returned if there are containers, and a 204 (No Content) code is returned if there are no containers.

To view the CDN container details, see :ref:`List metadata for CDN-enabled container <list-metadata-for-cdn-enabled-container>`.



This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |OK                       |The request succeeded.   |
|                          |                         |The information returned |
|                          |                         |with the response is     |
|                          |                         |dependent on the method  |
|                          |                         |used in the request.     |
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



This table shows the query parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|limit                     |Int *(Optional)*         |For an integer value n,  |
|                          |                         |limits the number of     |
|                          |                         |results to n values.     |
+--------------------------+-------------------------+-------------------------+
|marker                    |String *(Optional)*      |Given a string value x,  |
|                          |                         |returns container names  |
|                          |                         |greater in value than    |
|                          |                         |the specified marker.    |
|                          |                         |Only strings using UTF-8 |
|                          |                         |encoding are valid.      |
|                          |                         |Using ``marker``         |
|                          |                         |provides a mechanism for |
|                          |                         |iterating through the    |
|                          |                         |entire list of           |
|                          |                         |containers.              |
+--------------------------+-------------------------+-------------------------+
|end_marker                |String *(Optional)*      |Given a string value x,  |
|                          |                         |returns container names  |
|                          |                         |lesser in value than the |
|                          |                         |specified end marker.    |
|                          |                         |Only strings using UTF-8 |
|                          |                         |encoding are valid.      |
+--------------------------+-------------------------+-------------------------+
|format                    |String *(Optional)*      |Value of the serialized  |
|                          |                         |response format, either  |
|                          |                         |JSON or XML.             |
+--------------------------+-------------------------+-------------------------+




This operation does not accept a request body.




**Example: List CDN-enabled containers HTTP request**


.. code::

   GET /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123 HTTP/1.1
   Host: cdn.clouddrive.com
   X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c





**Example: List CDN-enabled containers HTTP request with a query parameter ?format=json​**


.. code::

   GET /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123?format=json HTTP/1.1
   Host: cdn.clouddrive.com
   X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c





Response
""""""""""""""""










**Example: List CDN-enabled containers HTTP response**


.. code::

   HTTP/1.1 200 OK
   Date: Thu, 08 Sep 2011 14:35:45 GMT
   Transfer-Encoding: chunked
   Content-Type: text/plain
                      
   images
   movies





**Example: List CDN-enabled containers HTTP response using a query parameter ?format=json​**


.. code::

   HTTP/1.1 200 OK
   Content-Length: 1985
   Content-Type: application/json
   X-Trans-Id: tx82a6752e00424edb9c46fa2573132e2c​iad3
   Date: Tue, 05 May 2015 14:09:02 GMT
   
   [
       {
           "cdn_enabled": true,
           "cdn_ios_uri": "http://acc3b9ba6a79805f5577-e7e60117100ffd73b45850c0b1fd96c1.iosr.cf5.rackcdn.com",
           "cdn_ssl_uri": "https://83c49b9a2f7ad18250b3-346eb45fd42c58ca13011d659bfc1ac1. ssl.cf0.rackcdn.com",
           "cdn_streaming_uri": "http://084cc2790632ccee0a12-346eb45fd42c58ca13011d659bfc1ac1. r49.stream.cf0.rackcdn.com",
           "cdn_uri": "http://081e40d3ee1cec5f77bf-346eb45fd42c58ca13011d659bfc1ac1.r49.cf0.rackcdn.com",
           "log_retention": false,
           "name": "cdn_test",
           "ttl": 259200
       },
       ...
   ]




