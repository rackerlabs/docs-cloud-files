.. _create-or-update-object:

Create or update object
~~~~~~~~~~~~~~~~~~~~~~~

.. code::

    PUT /v1/{account}/{container}/{object}

This operation creates or updates the content and metadata for a specified
object.

The ``PUT`` operation writes, or overwrites, an object's content and metadata.

.. note::
   The ``PUT`` operation actually always creates a new object. If you use this
   operation on an existing object, you actually replace the existing object
   and metadata rather than modifying the object. This is why this operation
   returns a ``201 (Created)`` status code.

You can ensure end-to-end data integrity by including an MD5 checksum of your
object's data in the ``ETag`` header. You are not required to include the
``ETag`` header, but we recommend its use to ensure that the storage system
successfully stores your object's content.

You can cause an object to expire after a certain date and time by using the
``X-Delete-At`` or ``X-Delete-After`` headers during an object ``PUT``
operation. The ``X-Delete-At`` header requires a Unix epoch timestamp, in
integer form. For example, 1348691905 represents Wed, 26 Sep 2012 20:38:25 GMT.
By setting the header to a specific epoch time, you indicate when you want the
object to expire, not be served, and be deleted completely from the storage
system. When Cloud Files detects one of these headers, the system automatically
stops serving that object at the specified date and time, and shortly after the
expiration date, it removes the object from the storage system.

The HTTP response includes the MD5 checksum of the data written to the storage
system. If you do not send the ``ETag`` header in the request, you should
compare the value returned with your content's MD5 locally to perform the
end-to-end data validation on the client side. For manifest objects, ``ETag``
is the MD5 checksum of the concatenated string of ETags for each segment in the
manifest, which offers change detection but not direct comparison.

For more information, see
:ref:`Creating large objects <creating-large-objects>`.

.. note::
   The best checks for a successful upload are to check the ``ETag`` match with
   a checksum and to see if you get a 404 (Not Found) status code when you
   perform a ``GET``, ``HEAD``, ``POST``, or ``DELETE`` operation.

You can assign custom metadata to objects by including additional HTTP headers
in the ``PUT`` request. To assign custom metadata, use an HTTP header with the
``X-Object-Meta-`` prefix.

You can also specify the ``Content-Type`` header for your object. For example,
you can specify ``Content-Type: audio/mpeg3`` for MP3 files.

A status code of ``201 (Created)`` indicates a successful write. Any status
code in the ``400`` range denotes failure. The ``401 (Unauthorized)`` status
code is returned if authentication fails. The ``411 (Length Required)`` status
code denotes a missing ``Content-Length`` or ``Content-Type`` header in the
request. If the MD5 checksum of the data written to the storage system does not
match the optionally supplied ``ETag`` value, a ``422 (Unprocessable Entity)``
status code is returned.

This table shows the possible response codes for this operation:

+-------------------------+-------------------------+-------------------------+
|Response Code            |Name                     |Description              |
+=========================+=========================+=========================+
|201                      |Created                  |The request has been     |
|                         |                         |fulfilled.               |
+-------------------------+-------------------------+-------------------------+
|202                      |Accepted                 |The request has been     |
|                         |                         |accepted for processing. |
+-------------------------+-------------------------+-------------------------+
|401                      |Unauthorized             |Authentication has       |
|                         |                         |failed.                  |
+-------------------------+-------------------------+-------------------------+
|411                      |Length Required          |The request did not      |
|                         |                         |specify the length of    |
|                         |                         |its content.             |
+-------------------------+-------------------------+-------------------------+
|422                      |Unprocessable Entity     |The request could not be |
|                         |                         |followed due to semantic |
|                         |                         |errors.                  |
+-------------------------+-------------------------+-------------------------+

Request
-------

This table shows the URI parameters for the request:

+-------------------------+-------------------------+-------------------------+
|Name                     |Type                     |Description              |
+=========================+=========================+=========================+
|{account}                |String                   |Your unique account      |
|                         |                         |identifier.              |
+-------------------------+-------------------------+-------------------------+
|{container}              |String                   |The unique identifier of |
|                         |                         |the container.           |
+-------------------------+-------------------------+-------------------------+
|{object}                 |String                   |The unique identifier of |
|                         |                         |the object.              |
+-------------------------+-------------------------+-------------------------+

This table shows the header parameters for the request:

+-------------------------+-------------------------+-------------------------+
|Name                     |Type                     |Description              |
+=========================+=========================+=========================+
|X-Auth-Token             |String *(Required)*      |Authentication token.    |
+-------------------------+-------------------------+-------------------------+
|ETag                     |String                   |The MD5 checksum of your |
|                         |                         |object's data.           |
+-------------------------+-------------------------+-------------------------+
|Content-Type             |String                   |The media type of the    |
|                         |                         |entity-body sent. If not |
|                         |                         |specified, the           |
|                         |                         |``Content-Type``         |
|                         |                         |is guessed, by           |
|                         |                         |using the Python         |
|                         |                         |mimetypes library, based |
|                         |                         |on the object path.      |
+-------------------------+-------------------------+-------------------------+
|Content-Length           |Int                      |Set to the length of the |
|                         |                         |object content. Do not   |
|                         |                         |set if chunked transfer  |
|                         |                         |encoding is being used.  |
+-------------------------+-------------------------+-------------------------+
|Content-Disposition      |String                   |The new browser behavior |
|                         |                         |for the file, so that    |
|                         |                         |the downloader can save  |
|                         |                         |the file rather than     |
|                         |                         |displaying it using      |
|                         |                         |default browser settings.|
+-------------------------+-------------------------+-------------------------+
|Content-Encoding         |String                   |The underlying media     |
|                         |                         |type of the compressed   |
|                         |                         |file.                    |
+-------------------------+-------------------------+-------------------------+
|Transfer-Encoding        |String                   |Set to ``chunked`` to    |
|                         |                         |enable chunked transfer  |
|                         |                         |encoding. If used, do    |
|                         |                         |not set the              |
|                         |                         |``Content-Length``       |
|                         |                         |header to a non-zero     |
|                         |                         |value.                   |
+-------------------------+-------------------------+-------------------------+
|X-Delete-At              |Int                      |The certain date, in the |
|                         |                         |format of a Unix epoch   |
|                         |                         |timestamp, when the      |
|                         |                         |object will be removed.  |
+-------------------------+-------------------------+-------------------------+
|X-Delete-After           |Int                      |The certain date, in the |
|                         |                         |format of a Unix epoch   |
|                         |                         |timestamp, after which   |
|                         |                         |the object will be       |
|                         |                         |removed.                 |
+-------------------------+-------------------------+-------------------------+
|X-Object-Meta-name       |String                   |The custom object        |
|                         |                         |metadata. The ``name``   |
|                         |                         |at the end of this       |
|                         |                         |header represents the    |
|                         |                         |name of your metadata.   |
+-------------------------+-------------------------+-------------------------+
|X-Detect-Content-Type    |Boolean                  |If you set this header   |
|                         |                         |to ``True``, the         |
|                         |                         |``Content-Type`` that is |
|                         |                         |sent in the request (if  |
|                         |                         |any) is ignored, and     |
|                         |                         |``Content-Type`` is      |
|                         |                         |guessed by using the     |
|                         |                         |Python mimetypes library |
|                         |                         |based on the object path.|
+-------------------------+-------------------------+-------------------------+
|X-Object-Manifest        |String                   |Set to specify that this |
|                         |                         |is a dynamic large       |
|                         |                         |object manifest object.  |
|                         |                         |The value is the         |
|                         |                         |container and object     |
|                         |                         |name prefix of the       |
|                         |                         |segment objects in the   |
|                         |                         |form container/prefix.   |
|                         |                         |You must UTF-8-encode    |
|                         |                         |and then URL-encode the  |
|                         |                         |names of the container   |
|                         |                         |and prefix before you    |
|                         |                         |include them in this     |
|                         |                         |header.                  |
+-------------------------+-------------------------+-------------------------+
|X-Copy-From              |String                   |If set, this is the name |
|                         |                         |of an object used to     |
|                         |                         |create the new object by |
|                         |                         |copying the              |
|                         |                         |``X-Copy-From``          |
|                         |                         |object. The value        |
|                         |                         |is in form               |
|                         |                         |``container/object``.    |
|                         |                         |You must UTF-8-encode    |
|                         |                         |and then URL-encode the  |
|                         |                         |names of the container   |
|                         |                         |and object before you    |
|                         |                         |include them in the      |
|                         |                         |header. Using the PUT    |
|                         |                         |operation with           |
|                         |                         |``X-Copy-From``          |
|                         |                         |has the same             |
|                         |                         |effect as using the COPY |
|                         |                         |operation to copy an     |
|                         |                         |object.                  |
+-------------------------+-------------------------+-------------------------+
|X-Copy-From-Account      |String                   |Used for account to      |
|                         |                         |account copy. Specifies  |
|                         |                         |the account name from    |
|                         |                         |which you want to copy   |
|                         |                         |an object. (The account  |
|                         |                         |name is the last part of |
|                         |                         |the storage URL).        |
+-------------------------+-------------------------+-------------------------+

This table shows the query parameters for the request:

+---------------+----------------+--------------------------------------------+
|Name           |Type            |Description                                 |
+===============+================+============================================+
|signature      |String          |Used with temporary URLs to sign the        |
|               |                |request. For more information about         |
|               |                |temporary URLs, see :ref:`TempURL<tempurl>`.|
+---------------+----------------+--------------------------------------------+
|expires        |String          |Used with temporary URLs to specify the     |
|               |                |expiry time of the signature. For more      |
|               |                |information about temporary URLs, see       |
|               |                |:ref:`TempURL<tempurl>`.                    |
+---------------+----------------+--------------------------------------------+
|multipart-     |String          |If you include the                          |
|               |                |``multipart-manifest=get``                  |
|               |                |query parameter and the                     |
|               |                |object is a large object, the object        |
|               |                |contents are not returned. Instead, the     |
|               |                |manifest is returned in the                 |
|               |                |``X-Object-Manifest``                       |
|               |                |response header for dynamic                 |
|               |                |large objects or in the response body for   |
|               |                |static large objects.                       |
+---------------+----------------+--------------------------------------------+

This operation does not accept a request body.

**Example: Create or update object HTTP request**

.. code::

   PUT /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer/MyObject HTTP/1.1
   Host: storage.clouddrive.com
   X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c
   ETag: 8a964ee2a5e88be344f36c22562a6486
   Content-Length: 512000
   X-Delete-At: 1339429105
   Content-Disposition: attachment; filename=platmap.mp4
   Content-Type: video/mp4
   Content-Encoding: gzip
   X-Object-Meta-PIN: 1234

Response
--------

This table shows the header parameters for the response:

+-------------------------+-------------------------+-------------------------+
|Name                     |Type                     |Description              |
+=========================+=========================+=========================+
|Content-Length           |String                   |If the operation         |
|                         |                         |succeeds, this value is  |
|                         |                         |zero (0). If the         |
|                         |                         |operation fails, this    |
|                         |                         |value is the length of   |
|                         |                         |the error text in the    |
|                         |                         |response body.           |
+-------------------------+-------------------------+-------------------------+
|Etag                     |String                   |For objects smaller than |
|                         |                         |5 GB, this value is the  |
|                         |                         |MD5 checksum of the      |
|                         |                         |uploaded object content. |
|                         |                         |The value is not quoted. |
|                         |                         |If you supplied an ETag  |
|                         |                         |request header and the   |
|                         |                         |operation was            |
|                         |                         |successful, the values   |
|                         |                         |are the same. If you did |
|                         |                         |not supply an ETag       |
|                         |                         |request header, check    |
|                         |                         |the ETag response header |
|                         |                         |value against the object |
|                         |                         |content you have just    |
|                         |                         |uploaded. For static     |
|                         |                         |large objects, this      |
|                         |                         |value is the MD5         |
|                         |                         |checksum of the          |
|                         |                         |concatenated string of   |
|                         |                         |MD5 checksums and ETags  |
|                         |                         |for each of the segments |
|                         |                         |in the manifest, and not |
|                         |                         |the MD5 checksum of the  |
|                         |                         |content that was         |
|                         |                         |uploaded. Also the value |
|                         |                         |is enclosed in double-   |
|                         |                         |quotes. For dynamic      |
|                         |                         |large objects, the value |
|                         |                         |is the MD5 checksum of   |
|                         |                         |the empty string.        |
+-------------------------+-------------------------+-------------------------+
|Content-Type             |String                   |The MIME type of the     |
|                         |                         |object.                  |
+-------------------------+-------------------------+-------------------------+
|X-Trans-Id               |Uuid                     |A unique transaction     |
|                         |                         |identifier for this      |
|                         |                         |request.                 |
+-------------------------+-------------------------+-------------------------+
|Date                     |Datetime                 |The transaction date and |
|                         |                         |time.                    |
+-------------------------+-------------------------+-------------------------+

This operation does not return a response body.

**Example: Create or update object HTTP response**

.. code::

   HTTP/1.1 201 Created
   Last-Modified: Fri, 17 Jan 2014 17:28:35 GMT
   Content-Length: 116
   Etag: 8a964ee2a5e88be344f36c22562a6486
   Content-Type: text/html; charset=UTF-8
   X-Trans-Id: tx4d5e4f06d357462bb732f-0052d96843
   Date: Fri, 17 Jan 2014 17:28:35 GMT
