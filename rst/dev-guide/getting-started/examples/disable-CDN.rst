.. _gsg-disable-cdn:

Disabling CDN for a container
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To disable use of the CDN for a container, you send an HTTP **POST**
request with a valid authentication token and with
``X-CDN-Enabled: False`` to the CDN management service. (Note that the
service access endpoint URL specifies the CDN system.)

An HTTP status code of 202 (Accepted) in the response indicates that the
request is accepted for processing.

 
**cURL disable CDN for a container request**

.. code::  

   curl -i -X POST $API_ENDPOINT/v1/$TENANT_ID/yourContainerName \
   -H "X-Auth-Token: $AUTH_TOKEN" \
   -H "X-CDN-Enabled: False"

**Disable CDN for a container response**

.. code::  

   HTTP/1.1 202 Accepted
   Content-Length: 76
   X-Cdn-Ssl-Uri: https://d0bba87ecb20cfe87c32-58d9a15a50acf66d588aab08348cf859.ssl.cf6.rackcdn.com
   X-Cdn-Ios-Uri: http://d03710c19b61b2c12609-58d9a15a50acf66d588aab08348cf859.iosr.cf6.rackcdn.com
   X-Cdn-Uri: http://afab448ae0b809160b64-58d9a15a50acf66d588aab08348cf859.r57.cf6.rackcdn.com
   Content-Type: text/html; charset=UTF-8
   X-Cdn-Streaming-Uri: http://499c627df9227c250afb-58d9a15a50acf66d588aab08348cf859.r57.stream.cf6.rackcdn.com
   X-Trans-Id: tx9f451de144d04250a96ed-00535a969bhkg1
   Date: Fri, 25 Apr 2014 17:08:43 GMT
