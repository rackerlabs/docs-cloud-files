
.. THIS OUTPUT IS GENERATED FROM THE WADL. DO NOT EDIT.

Get object content and metadata
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /v1/{account}/{container}/{object}

Gets the content and metadata for the object.

Perform ``GET`` operations against an object to retrieve the object's data. 

You can perform conditional ``GET`` requests by using the following HTTP headers in the request:



*  ``If-Match``
*  ``If-None-Match``
*  ``If-Modified-Since``
*  ``If-Unmodified-Since``


These headers are documented in `http://www.ietf.org/rfc/rfc2616.txt <http://www.ietf.org/rfc/rfc2616.txt>`__.

You can fetch a portion of the data by using the HTTP ``Range`` header. To specify multiple ranges, separate the range specifications with a comma.

The types of range specifications are as follows:



*  Byte range specification: Use a ``FIRST_BYTE_OFFSET`` value to specify the start of the data range, and use a ``LAST_BYTE_OFFSET`` value to specify the end of the range. If you omit the LAST_BYTE_OFFSET value, the offset of the last byte of data is used
*  Suffix byte range specification: Use ``LENGTH`` bytes to specify the length of the data range.


The following table shows forms of the header and the ranges of data specified.

Cloud Files supported range formatsHeaderRange of Object Data``Range: bytes=-5``The last five bytes.``Range: bytes=10-15``The six bytes of data after a 10-byte offset.``Range: bytes=10-15,-5``A multipart response that contains the last five bytes and the six bytes of data after a 10-byte offset. The ``Content-Type`` of the response is then ``multipart/byteranges``.``Range: bytes=4-6``Bytes 4 through 6.``Range: bytes=2-2``Byte 2, the third byte of the data.``Range: bytes=6-``Byte 6 and after.``Range: bytes=1-3,2-5``A multipart response that contains bytes 1 through 3, and bytes 2 through 5. The ``Content-Type`` of the response is then ``multipart/byteranges``.

Object data is returned in the response body. Object metadata is returned as HTTP headers. 

A status code of 200 through 299 indicates success. Status code 404 (Not Found) is returned if the object does not exist.

.. note::
   In the following examples that use ranges, the object contains the 10 bytes of data 0123456789.
   
   



This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |OK                       |The request has          |
|                          |                         |succeeded. The           |
|                          |                         |information returned     |
|                          |                         |with the response is     |
|                          |                         |dependent on the method  |
|                          |                         |used in the request.     |
+--------------------------+-------------------------+-------------------------+
|404                       |Not Found                |The requested resource   |
|                          |                         |was not found.           |
+--------------------------+-------------------------+-------------------------+


Request
""""""""""""""""

This table shows the URI parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|{account}                 |String                   |Your unique account      |
|                          |                         |identifier.              |
+--------------------------+-------------------------+-------------------------+
|{container}               |String                   |The unique identifier of |
|                          |                         |the container.           |
+--------------------------+-------------------------+-------------------------+
|{object}                  |String                   |The unique identifier of |
|                          |                         |the object.              |
+--------------------------+-------------------------+-------------------------+



This table shows the query parameters for the request:

+----------------+----------------+--------------------------------------------+
|Name            |Type            |Description                                 |
+================+================+============================================+
|signature       |String          |Used with temporary URLs to sign the        |
|                |*(Optional)*    |request. For more information about         |
|                |                |temporary URLs, see `TempURL                |
|                |                |<http://docs.rackspace.com/files/api/v1/cf- |
|                |                |devguide/content/TempURL-d1a4450.html>`__.  |
+----------------+----------------+--------------------------------------------+
|expires         |String          |Used with temporary URLs to specify the     |
|                |*(Optional)*    |expiry time of the signature. For more      |
|                |                |information about temporary URLs, see       |
|                |                |`TempURL                                    |
|                |                |<http://docs.rackspace.com/files/api/v1/cf- |
|                |                |devguide/content/TempURL-d1a4450.html>`__.  |
+----------------+----------------+--------------------------------------------+
|multipart-      |String          |If you include the``multipart-              |
|manifest        |*(Optional)*    |manifest=get`` query parameter and the      |
|                |                |object is a large object, the object        |
|                |                |contents are not returned. Instead, the     |
|                |                |manifest is returned in the``X-Object-      |
|                |                |Manifest`` response header for dynamic      |
|                |                |large objects or in the response body for   |
|                |                |static large objects.                       |
+----------------+----------------+--------------------------------------------+




This operation does not accept a request body.




**Example Get object data: HTTP request**


.. code::

    GET /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer/MyObject HTTP/1.1
    Host: storage.clouddrive.com
    X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c


**Example Get object data using a range: HTTP request**


.. code::

    GET /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer/MyObject HTTP/1.1
    Host: storage.clouddrive.com
    X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c
    Range: bytes=4-6


**Example Get object data using multiple ranges: HTTP request**


.. code::

    GET /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer/MyObject HTTP/1.1
    Host: storage.clouddrive.com
    X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c
    Range: bytes=1-3,2-5


Response
""""""""""""""""





**Example Get object data response**


.. code::

    HTTP/1.1 200 OK
    Date: Wed, 14 Jul 2010 19:37:41 GMT
    Last-Modified: Mon, 12 Jun 2010 13:40:18 GMT
    ETag: b0dffe8254d152d8fd28f3c5e0404a10
    Content-Type: text/html
    Content-Length: 512000
    
    [ ...object content... ]


**Example Get object data using range response**


.. code::

    HTTP/1.1 206 Partial Content
    Date: Wed, 14 Jul 2010 19:37:41 GMT
    Last-Modified: Mon, 12 Jun 2010 13:40:18 GMT
    ETag: b0dffe8254d152d8fd28f3c5e0404a10
    Content-Type: application/octet-stream
    Accept-Ranges: bytes
    Content-Range: bytes 4-6/10
    Content-Length: 3
    
    456


**Example Get object data using multiple ranges response**


.. code::

    HTTP/1.1 206 Partial Content
    Date: Wed, 14 Jul 2010 19:37:41 GMT
    Last-Modified: Mon, 12 Jun 2010 13:40:18 GMT
    ETag: b0dffe8254d152d8fd28f3c5e0404a10
    Content-Type: multipart/byteranges;boundary=4789b20f24cc4d2a8da2e552e151e6fe
    Accept-Ranges: bytes
    Content-Range: bytes 4-6/10
    Content-Length: 265
    
    --4789b20f24cc4d2a8da2e552e151e6fe
    Content-Type: application/octet-stream
    Content-Range: bytes 1-3/10
    
    123
    --4789b20f24cc4d2a8da2e552e151e6fe
    Content-Type: application/octet-stream
    Content-Range: bytes 2-5/10
    
    2345
    --4789b20f24cc4d2a8da2e552e151e6fe--
    


