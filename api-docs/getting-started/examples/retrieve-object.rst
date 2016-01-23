.. _gsg-retrieve-object:

Retrieving an object
~~~~~~~~~~~~~~~~~~~~

To get the object content and metadata, you send an HTTP **GET** request
with a valid authentication token.

An HTTP status code of 200 (OK) in the response indicates that the
object was successfully retrieved.

 
**cURL retrieve an object request**

.. code::  

   curl -i -X GET $API_ENDPOINT/v1/$TENANT_ID/yourContainerName/yourObjectName \
   -H "X-Auth-Token: $AUTH_TOKEN" 

**Retrieve an object response**

.. code::  

   HTTP/1.1 200 OK
   Content-Length: 0
   Accept-Ranges: bytes
   X-Object-Meta-Imagetype: png
   Last-Modified: Tue, 22 Apr 2014 17:06:52 GMT
   X-Object-Meta-Imagesize: 400 MB
   Etag: d41d8cd98f00b204e9800998ecf8427e
   X-Timestamp: 1398186411.61064
   Content-Type: image/jpeg
   X-Trans-Id: txad3571ebcee24cabb387a-005356a229dfw1
   Date: Tue, 22 Apr 2014 17:08:57 GMT 

    [ ...object content...]
