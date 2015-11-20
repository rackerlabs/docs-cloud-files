.. _gsg-view-cdn-container-details:

Viewing CDN-enabled container details
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To view details about a container in the CDN, you send an HTTP **HEAD**
request with a valid authentication token to the CDN management service.

An HTTP status code of 204 (No Content) in the response indicates that
the container details were successfully retrieved. You can confirm the
TTL that you set in :ref:`CDN-enabling the container and setting a
TTL <gsg-cdn-enabling-container>`.

 
**Example: cURL view CDN-enabled container details**

.. code::  

   curl -i -X HEAD https://cdn1.clouddrive.com/v1/yourAccountID/yourContainerName /
   -H "X-Auth-Token: yourAuthToken" 

.. code::  

   HTTP/1.1 204 No Content
   Content-Length: 0
   X-Cdn-Ssl-Uri: https://c93f9b29cd3c6bd865ee-24695493c49b279502b280c6ecd262b5.ssl.cf6.rackcdn.com
   X-Ttl: 604800
   X-Cdn-Enabled: True
   X-Log-Retention: False
   X-Cdn-Ios-Uri: http://7a701469fe9980c577e9-24695493c49b279502b280c6ecd262b5.iosr.cf6.rackcdn.com
   X-Cdn-Uri: http://98199d7b2503ac330f05-24695493c49b279502b280c6ecd262b5.r17.cf6.rackcdn.com
   Content-Type: text/html; charset=UTF-8
   X-Cdn-Streaming-Uri: http://ce3a54aaf724a75455d6-24695493c49b279502b280c6ecd262b5.r17.stream.cf6.rackcdn.com
   X-Trans-Id: txe291eebdfd96468995a80-005356b167hkg1
   Date: Tue, 22 Apr 2014 18:13:59 GMT
