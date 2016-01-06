.. _gsg-upload-storage-object:

Uploading an object 
~~~~~~~~~~~~~~~~~~~~~~~~

After creating a container, you can upload a file to it.

To upload an object, you send an HTTP **PUT** request with a valid
authentication token.

You must ensure that the object's ``Content-Type`` is set correctly so
that the receiving server knows what kind of file it is. For more
information about ``Content-Type``, see the `Header Field Definitions in
the Hypertext Transfer
Protocol <http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html>`__.
This is the mechanism by which a user's web browser knows how to display
the file or whether to launch a helper application to display the file.

If you know the value of ``Content-Length``, you should also set it in the
request. However, when you send the file in the cURL request by using the 
cURL ``-T`` option, cURL, by default, sets the ``Content-Length`` 
correctly by reading the file. In this case, you can omit ``Content-Length`` 
in the request.

An HTTP status code of 201 (Created) in the response indicates that the
object was successfully uploaded.

 
**cURL upload an object request**

.. code::  

   curl -i -X PUT $API_ENDPOINT/v1/$TENANT_ID/yourContainerName/yourObjectName \
   -H "X-Auth-Token: $AUTH_TOKEN" \
   -H "Content-Type: image/jpeg” \
   -H "Content-Length: 0"

**Upload an object response**

.. code::  

   HTTP/1.1 201 Created
   Last-Modified: Wed, 06 Jan 2016 17:08:31 GMT
   Content-Length: 0
   Etag: d41d8cd98f00b204e9800998ecf8427e
   Content-Type: text/html; charset=UTF-8
   X-Trans-Id: tx8c18c3e63d2f4c61b9cbe-00568d4a0edfw1
   Date: Wed, 06 Jan 2016 17:08:31 GMT
