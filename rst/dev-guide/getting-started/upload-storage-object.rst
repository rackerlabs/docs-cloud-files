.. _gsg-upload-storage-object:

Upload an object 
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

An HTTP status code of 201 (Created) in the response indicates that the
object was successfully uploaded.

 
**Example: cURL upload an object**

.. code::  

   curl -i -X PUT https://storage101.dfw1.clouddrive.com/v1/yourAccountID/yourContainerName/yourObjectName /
   -H "X-Auth-Token: yourAuthToken" \
   -H "Content-Type: image/jpeg" \
   -H "Content-Length: 0"

.. code::  

   HTTP/1.1 201 Created
   Last-Modified: Tue, 22 Apr 2014 17:02:35 GMT
   Content-Length: 0
   Etag: d41d8cd98f00b204e9800998ecf8427e
   Content-Type: text/html; charset=UTF-8
   X-Trans-Id: tx4f2953d5969d4c40ada04-005356a0aadfw1
   Date: Tue, 22 Apr 2014 17:02:34 GMT
