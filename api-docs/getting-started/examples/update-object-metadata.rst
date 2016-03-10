.. _gsg-update-object-metadata:

Updating object metadata
~~~~~~~~~~~~~~~~~~~~~~~~

To set or update custom metadata for existing objects, you send an HTTP
**POST** request with a valid authentication token. Metadata is set by
using the header ``X-Object-Meta-name: value``, where name is the custom
name for your metadata and value is the data value.

..  note:: 
    If an object has custom metadata, when you post new metadata, you must
    resend any metadata that you want kept with the object or it will be
    lost.

An HTTP status code of 202 (Accepted) in the response indicates that the
metadata for the object was successfully updated.

 
**Example: cURL update object metadata request**

.. code::  

   curl -i -X POST $API_ENDPOINT/v1/$TENANT_ID/yourContainerName/yourObjectName \
   -H "X-Auth-Token: $AUTH_TOKEN" \
   -H "X-Object-Meta-ImageType: png" \
   -H "X-Object-Meta-ImageSize: 400 MB"

**Example: Update object metadata response**

.. code::  

   HTTP/1.1 202 Accepted
   Content-Length: 76
   Content-Type: text/html; charset=UTF-8
   X-Trans-Id: txffc66e0337ae4cd19e79c-005356a1abdfw1
   Date: Tue, 22 Apr 2014 17:06:51 GMT
