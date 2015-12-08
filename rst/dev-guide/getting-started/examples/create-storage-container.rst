.. _gsg-create-storage-container:

Creating a storage container
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Before uploading any data to Cloud Files, you must create a storage
container.

To create a container, you send an HTTP **PUT** request with a valid
authentication token.

An HTTP status code of 201 (Created) in the response indicates that the
container was successfully created.

 
**cURL create a storage container request**

.. code::  

   curl -i -X PUT $API_ENDPOINT/v1/$TENANT_ID/yourContainerName \
   -H "X-Auth-Token: $AUTH_TOKEN" 

**Create a storage container response**

.. code::  

   HTTP/1.1 201 Created
   Content-Length: 0
   Content-Type: text/html; charset=UTF-8
   X-Trans-Id: txfaf60e1d2a844e5ca9998-0053569d54dfw1
   Date: Tue, 22 Apr 2014 16:48:21 GMT