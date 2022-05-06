.. _gsg-cdn-enabling-container:

CDN-enabling the container and setting a TTL
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

After creating a container and storing a file in it, you can choose to
make the file publicly readable. Because the data in Cloud Files is
private, you share your files through the content delivery network
(CDN).

To CDN-enable a container, you send an HTTP **PUT** request with a valid
authentication token and with ``X-CDN-Enabled: True`` to the CDN
management service. (Note that the service access endpoint URL specifies
the CDN system.) The default time to live (TTL) value is 72 hours
(259200 seconds), with a minimum of 15 minutes (900 seconds) and a
maximum of 1 year (31536000 seconds). The following request sets the TTL
to 1 week (604800 seconds) with ``X-TTL:                 604800``.

An HTTP status code of 201 (Created) in the response indicates that the
container was successfully CDN-enabled.

When the container is CDN-enabled, the service returns its public URI in
the ``X-Cdn-Uri`` header of the response, and returns the SSL URI in the
``X-Cdn-Ssl-Uri`` header of the response. You can combine the public URI
with the object name to access the file through the CDN, or you can use
the SSL URI with the object name to access the file over a secure SSL
connection through the CDN.
 
**Example: cURL CDN-enable container and set TTL request**

.. code::

   curl -i -X PUT $API_ENDPOINT/v1/$TENANT_ID/yourContainerName \
   -H "X-Auth-Token: $AUTH_TOKEN" \
   -H "X-CDN-Enabled: True" \
   -H "X-TTL: 604800"

**Example: CDN-enable container and set TTL response**

**Note:** X-Cdn-Streaming-Uri and X-Cdn-Ios-Uri links will be discontinued on July 31, 2022.

.. code::

   HTTP/1.1 201 Created
   Content-Length: 0
   X-Cdn-Ssl-Uri: https://c93f9b29cd3c6bd865ee-24695493c49b279502b280c6ecd262b5.ssl.cf6.rackcdn.com
   X-Cdn-Ios-Uri: http://7a701469fe9980c577e9-24695493c49b279502b280c6ecd262b5.iosr.cf6.rackcdn.com
   X-Cdn-Uri: http://98199d7b2503ac330f05-24695493c49b279502b280c6ecd262b5.r17.cf6.rackcdn.com
   Content-Type: text/html; charset=UTF-8
   X-Cdn-Streaming-Uri: http://ce3a54aaf724a75455d6-24695493c49b279502b280c6ecd262b5.r17.stream.cf6.rackcdn.com
   X-Trans-Id: txc2b9b4ef77fd45f28c2d2-005356adfchkg1
   Date: Tue, 22 Apr 2014 17:59:24 GMT
