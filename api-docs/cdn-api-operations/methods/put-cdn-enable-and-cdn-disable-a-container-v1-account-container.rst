.. _put-cdn-enable-and-cdn-disable-a-container:

CDN-enable and CDN-disable a container
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    PUT /v1/{account}/{container}

This operation enables or disables a container for use with the CDN.

Before a container can be CDN-enabled, it must exist in the storage system. To
CDN-enable the container, perform a ``PUT`` request against it using the
``publicURL`` noted in the service catalog with  ``"name": "cloudFilesCDN"``
during authentication, and set the ``X-CDN-Enabled`` header to ``True``.

The :ref:`Authentication <auth>` section provides an example of the information
in the service catalog for ``cloudFilesCDN``.

When a container is CDN-enabled, any objects stored in it are publicly
accessible over the CDN by combining the container's CDN URI with the object
name ( ``X-Cdn-Uri/objectName``).

.. note::
   The examples in this guide use ``cdn.clouddrive.com`` as the endpoint for
   operations against the CDN management service, but you should use whatever
   endpoints your authentication request provides. For more information about
   service access endpoints, see
   :ref:`Service access endpoints <service-access>`.

Any CDN-accessed objects are cached in the CDN for a specified amount of time,
called the Time To Live (TTL). Each time the object is accessed after the TTL
expires, the CDN refetches and caches the object for the next TTL period.

You can specify the TTL for an object by including the
``X-Ttl: integerSeconds`` header. Setting the TTL is the same as setting the
``Expires`` and ``Cache-Control`` headers for the cached object. The minimum
TTL is 15 minutes (900 seconds), the maximum TTL is 1 year (31536000 seconds),
and the default TTL is 72 hours (259200 seconds). However, setting a TTL for a
long time does not guarantee that the content stays populated on CDN edge
servers for the entire period. The most popular objects stay cached based on
the edge location's logic.

A status code of 201 (Created) indicates that the container was CDN-enabled as
requested. If the container is already CDN-enabled, a 202 (Accepted) status
code is returned, and the TTL is adjusted. A status code of 204 (No Content)
indicates that the container was CDN-enabled as requested but has no content.

This operation does not require a request body and does not return a response
body.

To remove the container from the CDN, change the ``X-Cdn-Enabled`` header to
``False``. However, note that objects remain on the CDN edge server and are
served to the public until their TTL expires.

.. note::
   The CDN URI is unique per container. After the container is CDN-enabled, you
   can make a ``HEAD`` request to the Cloud Files CDN endpoint with the
   container name to return the CDN URI in the ``X-Cdn-Uri`` header. You can
   use a cURL request similar to the following example:
   ``curl -I -H 'x-auth-token: yourAuthToken' cloudFilesCDN:yourPublicURL/yourContainerName``

This table shows the possible response codes for this operation:

+--------------------------+-------------------------+------------------------+
|Response Code             |Name                     |Description             |
+==========================+=========================+========================+
|200                       |OK                       |The request has         |
|                          |                         |succeeded.              |
+--------------------------+-------------------------+------------------------+
|202                       |Accepted                 |The request has been    |
|                          |                         |accepted for processing.|
+--------------------------+-------------------------+------------------------+
|204                       |No Content               |The request succeeded.  |
|                          |                         |The server fulfilled the|
|                          |                         |request but does not    |
|                          |                         |need to return a body.  |
+--------------------------+-------------------------+------------------------+
|404                       |Not Found                |The requested resource  |
|                          |                         |was not found.          |
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
|X-Ttl                     |Int                      |Specifies the Time To   |
|                          |                         |Live (TTL) in seconds   |
|                          |                         |for an object to be     |
|                          |                         |cached in the CDN. The  |
|                          |                         |default value is 259200 |
|                          |                         |seconds, or 72 hours.   |
|                          |                         |The minimum TTL is 15   |
|                          |                         |minutes (or 900         |
|                          |                         |seconds), and the       |
|                          |                         |maximum is 1 year       |
|                          |                         |(31536000 seconds).     |
+--------------------------+-------------------------+------------------------+
|X-Cdn-Enabled             |String                   |Indicates if a container|
|                          |                         |is CDN-enabled. Valid   |
|                          |                         |values are True and     |
|                          |                         |False.                  |
+--------------------------+-------------------------+------------------------+

This operation does not accept a request body.

**Example: CDN-enable container HTTP request**

.. code::

   PUT /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer HTTP/
   1.1
   Host: cdn.clouddrive.com
   X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c
   X-Ttl: 259200
   X-Cdn-Enabled: True

**Example: CDN-disable container HTTP request**

.. code::

   POST /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer HTTP/1.1
   Host: cdn.clouddrive.com
   X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c
   X-CDN-Enabled: False

Response
""""""""

This table shows the header parameters for the response:

+--------------------------+-------------------------+------------------------+
|Name                      |Type                     |Description             |
+==========================+=========================+========================+
|Content-Length            |String                   |If the operation        |
|                          |                         |succeeds, this value is |
|                          |                         |zero (0). If the        |
|                          |                         |operation fails, this   |
|                          |                         |value is the length of  |
|                          |                         |the error text in the   |
|                          |                         |response body.          |
+--------------------------+-------------------------+------------------------+
|Content-Type              |String                   |The MIME type of the    |
|                          |                         |list of names. If the   |
|                          |                         |operation fails, this   |
|                          |                         |value is the MIME type  |
|                          |                         |of the error text in the|
|                          |                         |response body.          |
+--------------------------+-------------------------+------------------------+
|Date                      |Datetime                 |The transaction date and|
|                          |                         |time.                   |
+--------------------------+-------------------------+------------------------+
|X-Cdn-Ios-Uri             |String                   |The URI for video       |
|                          |                         |streaming that uses HTTP|
|                          |                         |Live Streaming from     |
|                          |                         |Apple.                  |
+--------------------------+-------------------------+------------------------+
|X-Cdn-Ssl-Uri             |String                   |The URI for downloading |
|                          |                         |the object over HTTPS,  |
|                          |                         |using SSL. (The user    |
|                          |                         |cannot have custom SSL  |
|                          |                         |certificates because the|
|                          |                         |Rackspace CDN partner   |
|                          |                         |does not provide that   |
|                          |                         |feature.)               |
+--------------------------+-------------------------+------------------------+
|X-Cdn-Streaming-Uri       |String                   |The URI for video       |
|                          |                         |streaming that uses HTTP|
|                          |                         |Dynamic Streaming from  |
|                          |                         |Adobe.                  |
+--------------------------+-------------------------+------------------------+
|X-Cdn-Uri                 |String                   |Indicates the URI that  |
|                          |                         |you can combine with    |
|                          |                         |object names to serve   |
|                          |                         |objects through the CDN.|
+--------------------------+-------------------------+------------------------+
|X-Trans-Id                |Uuid                     |A unique transaction    |
|                          |                         |identifier for this     |
|                          |                         |request.                |
+--------------------------+-------------------------+------------------------+

This operation does not return a response body.

**Example: CDN-enable container HTTP response**

.. code::

   HTTP/1.1 204 No Content
   Content-Length: 0
   Content-Type →text/html; charset=UTF-8
   Date →Wed, 17 Dec 2014 19:58:49 GMT
   X-Cdn-Ios-Uri →http://acc3b9ba6a79805f5577-e7e60117100ffd73b45850c0b1fd96c1.iosr.cf5.rackcdn.com
   X-Cdn-Ssl-Uri: https://83c49b9a2f7ad18250b3-346eb45fd42c58ca13011d659bfc1ac1. ssl.cf0.rackcdn.com
   X-Cdn-Streaming-Uri: http://084cc2790632ccee0a12-346eb45fd42c58ca13011d659bfc1ac1. r49.stream.cf0.rackcdn.com
   X-Cdn-Uri: http://081e40d3ee1cec5f77bf-346eb45fd42c58ca13011d659bfc1ac1.r49.cf0.rackcdn.com
   X-Trans-Id: tx82a6752e00424edb9c46fa2573132e2c
