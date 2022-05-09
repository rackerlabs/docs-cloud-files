.. _streaming-cdn-enabled-containers:

Streaming CDN-enabled containers
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Note: X-Cdn-Streaming-Uri and X-Cdn-Ios-Uri links will be discontinued on July 31, 2022.**

In addition to the other headers associated with CDN, a **HEAD**
operation against a CDN-enabled container returns the following
streaming URIs to enable the streaming feature:

-  ``X-Cdn-Streaming-Uri``, which specifies a URI for video streaming
   that uses HTTP Dynamic Streaming from Adobe

-  ``X-Cdn-Ios-Uri``, which specifies the URI for video streaming that
   uses HTTP Live Streaming from Apple

Streaming is a method of relaying data, such as video and audio
material, over the network as a steady continuous stream, allowing
playback to proceed while subsequent data is being received.

For information about streaming to iOS devices, see
:ref:`iOS streaming <ios-streaming>`.

**Example: CDN-enabled container metadata: HTTP request**

.. code::

    HEAD /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer HTTP/1.1
    Host: cdn.clouddrive.com
    X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c

**Example: CDN-enabled container metadata with streaming URIs: HTTP
response**

.. code::

    HTTP/1.1 204 No Content
    X-Cdn-Ssl-Uri: https://83c49b9a2f7ad18250b3-346eb45fd42c58ca13011d659bfc1ac1. ssl.cf0.rackcdn.com
    X-Ttl: 259200
    X-Cdn-Ios-Uri: http://fb1ca9de5ff9525ff6f8-64e65126753c56b595824f56d25789bb.iosr.cf1.rackcdn.com
    X-Cdn-Streaming-Uri: http://084cc2790632ccee0a12-346eb45fd42c58ca13011d659bfc1ac1. r49.stream.cf0.rackcdn.com
    X-Cdn-Enabled: True
    X-Cdn-Ssl-Uri: https://2cb7edde3eac1dd66ea4-64e65126753c56b595824f56d25789bb.ssl.cf1.rackcdn.com
    X-Cdn-Uri: http://081e40d3ee1cec5f77bf-346eb45fd42c58ca13011d659bfc1ac1. r49.cf0.rackcdn.co
    X-Log-Retention: False
    X-Trans-Id: tx82a6752e00424edb9c46fa2573132e2c
    Content-Length: 0
