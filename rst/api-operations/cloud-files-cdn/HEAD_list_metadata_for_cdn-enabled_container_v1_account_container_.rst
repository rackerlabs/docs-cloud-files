=============================================================================
List Metadata For Cdn-Enabled Container -  Rackspace Cloud Files™ Developer Guide
=============================================================================

List Metadata For Cdn-Enabled Container
~~~~~~~~~~~~~~~~~~~~~~~~~

`Request <HEAD_list_metadata_for_cdn-enabled_container_v1_account_container_.rst#request>`__
`Response <HEAD_list_metadata_for_cdn-enabled_container_v1_account_container_.rst#response>`__

.. code-block:: javascript

    HEAD /v1/{account}/{container}

Gets a CDN-enabled container's metadata.

You can view CDN-enabled container details by performing a ``HEAD`` operation on a container where the ``Host`` header value is one of the ``cdnCloudFiles`` service access endpoints. (For the CDN endpoints, see `Service access endpoints <http://docs.rackspace.com/files/api/v1/cf-devguide/content/Service-Access-Endpoints-d1e003.html>`__.)

If the container is (or ever has been) CDN-enabled, the metadata is returned in headers in the response for plain text, or in the response body for XML or JSON, if you request either as your output format.

Remember that your ``HEAD`` operation must be on the CDN host (for example, ``cdn.clouddrive.com`` ). Otherwise, you will see the metadata for your private container as described in `Get account metadata <http://docs.rackspace.com/files/api/v1/cf-devguide/content/HEAD_retrieveaccountmeta_v1__account__accountServicesOperations_d1e000.html>`__.

A 204 (No Content) HTTP status code is returned if the account has no containers. Otherwise, the status code of 200 (OK) is returned. Status code 404 (Not Found) is returned if the requested container was not found.



This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |OK                       |The request has          |
|                          |                         |succeeded.The            |
|                          |                         |information returned     |
|                          |                         |with the response        |
|                          |                         |isdependent on the       |
|                          |                         |method used in           |
|                          |                         |therequest.The URI for   |
|                          |                         |downloading the object   |
|                          |                         |over HTTP. This URI can  |
|                          |                         |be combined with any     |
|                          |                         |object name within the   |
|                          |                         |container to form the    |
|                          |                         |publicly accessible URI  |
|                          |                         |for that object for      |
|                          |                         |distribution over a CDN  |
|                          |                         |system. The TTL value in |
|                          |                         |seconds. The default     |
|                          |                         |value is 259200 seconds, |
|                          |                         |or 72 hours. The minimum |
|                          |                         |TTL is 15 minutes (or    |
|                          |                         |900 seconds), and the    |
|                          |                         |maximum is 1 year        |
|                          |                         |(31536000 seconds). True |
|                          |                         |or False to indicate     |
|                          |                         |whether the container is |
|                          |                         |currently marked to      |
|                          |                         |allow public serving of  |
|                          |                         |objects through the CDN. |
|                          |                         |True or False to         |
|                          |                         |indicate whether the CDN |
|                          |                         |access logs should be    |
|                          |                         |collected and stored in  |
|                          |                         |the Cloud Files storage  |
|                          |                         |system. The URI for      |
|                          |                         |downloading the object   |
|                          |                         |over HTTPS, using SSL.   |
|                          |                         |(The user cannot have    |
|                          |                         |custom SSL certificates  |
|                          |                         |because the Rackspace    |
|                          |                         |CDN partner does not     |
|                          |                         |provide that feature.    |
|                          |                         |The URI for video        |
|                          |                         |streaming that uses HTTP |
|                          |                         |Dynamic Streaming from   |
|                          |                         |Adobe. The URI for video |
|                          |                         |streaming that uses HTTP |
|                          |                         |Live Streaming from      |
|                          |                         |Apple.                   |
+--------------------------+-------------------------+-------------------------+
|204                       |No Content               |The requestsucceeded.    |
|                          |                         |The server fulfilled the |
|                          |                         |request but doesnot need |
|                          |                         |to return a body.        |
+--------------------------+-------------------------+-------------------------+
|404                       |Not Found                |The requested resource   |
|                          |                         |was not found.           |
+--------------------------+-------------------------+-------------------------+


Request
^^^^^^^^^^^^^^^^^

This table shows the URI parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|{account}                 |xsd:string               |Your unique account      |
|                          |                         |identifier.              |
+--------------------------+-------------------------+-------------------------+
|{container}               |xsd:string               |The unique identifier of |
|                          |                         |the container.           |
+--------------------------+-------------------------+-------------------------+



This table shows the query parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|format                    |xsd:string *(Required)*  |The optional format for  |
|                          |                         |the returned             |
|                          |                         |information, either XML  |
|                          |                         |or JSON.                 |
+--------------------------+-------------------------+-------------------------+







**Example List metadata for CDN-enabled container: HTTP request**


.. code::

    HEAD /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer HTTP/1.1
    Host: cdn.clouddrive.com
    X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c
    


**Example List Metadata For Cdn-Enabled Container: JSON request**


.. code::

    HEAD /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer?format=json
    Host: cdn.clouddrive.com
    X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c


**Example List Metadata For Cdn-Enabled Container: XML request**


.. code::

    HEAD /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer?format=xml
    Host: cdn.clouddrive.com
    X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c


Response
^^^^^^^^^^^^^^^^^^





**Example Get CDN-enabled container metadata: HTTP request**


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


**Example List Metadata For Cdn-Enabled Container: JSON request**


.. code::

    HTTP/1.1 200 OK
    Date: Tue, 30 Oct 2012 14:41:29 GMT
    Content-Length: 127
    Content-Type: application/json; charset=utf-8
    [
     {"name":"test_container",
     "cdn_enabled":"true",
     "ttl":28800,
     "log_retention":"true",
     "cdn_uri":"http://80745c48926cd286a5a0-48261ebe0e4c795a565ece6b9cca2fe8.
     r10.cf1.rackcdn.com",
     "cdn_ssl_uri":"https://
     83c49b9a2f7ad18250b3-346eb45fd42c58ca13011d659bfc1ac1.ssl.stg2.rackcdn.com",
     "cdn_streaming_uri":"http://
     80745c48926cd286a5a0-48261ebe0e4c795a565ece6b9cca2fe8.r10.cf1.rackcdn.com"}
    ]


**Example List Metadata For Cdn-Enabled Container: XML request**


.. code::

    HTTP/1.1 200 OK
    Date: Tue, 30 Oct 2012 17:57:28 GMT
    Content-Length: 267
    Content-Type: application/xml; charset=utf-8
    <?xml version="1.0" encoding="UTF-8"?>
    <account name="WidgetsRUs.button">
      <container>
        <name>images</name>
        <cdn_enabled>True</cdn_enabled>
        <ttl>86400</ttl>
        <log_retention>True</log_retention>
          <cdn_url>
            http://80745c48926cd286a5a0-48261ebe0e4c795a565ece6b9cca2fe8.r10.
    cf1.rackcdn.com
          </cdn_url>
          <cdn_ssl_url>
            https://83c49b9a2f7ad18250b3-346eb45fd42c58ca13011d659bfc1ac1.ssl.
    stg2.rackcdn.com
          </cdn_ssl_url>
          <cdn_streaming_url>
            http://084cc2790632ccee0a12-346eb45fd42c58ca13011d659bfc1ac1. r49.
    stream.cf0.rackcdn.com
          </cdn_streaming_url>
      </container>
    </account>

