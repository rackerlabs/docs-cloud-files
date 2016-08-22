.. _cdn-enabled-containers-served-through-ssl:

CDN-enabled containers served through SSL
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A **HEAD** operation for a CDN-enabled container returns an SSL URI,
``X-Cdn-Ssl-Uri``, in addition to the other headers associated with CDN.
This feature enables you to use HTTPS protocol in URIs that are used for
requesting objects stored in CDN-enabled containers.

**Example: CDN-enabled container metadata: HTTP request**

.. code::

    HEAD /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer HTTP/1.1
    Host: cdn.clouddrive.com
    X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c

**Example: CDN-enabled container metadata with SSL URI: HTTP
response**

.. code::

    HTTP/1.1 204 No Content
    X-Cdn-Ssl-Uri: https://83c49b9a2f7ad18250b3-346eb45fd42c58ca13011d659bfc1ac1. ssl.cf0.rackcdn.com
    X-Ttl: 259200
    X-Cdn-Uri: http://081e40d3ee1cec5f77bf-346eb45fd42c58ca13011d659bfc1ac1. r49.cf0.rackcdn.com
    X-Cdn-Enabled: True
    X-Log-Retention: False
    X-Cdn-Streaming-Uri: http://084cc2790632ccee0a12-346eb45fd42c58ca13011d659bfc1ac1. r49.stream.cf0.rackcdn.com
    X-Trans-Id: tx82a6752e00424edb9c46fa2573132e2c
    Content-Length: 0
