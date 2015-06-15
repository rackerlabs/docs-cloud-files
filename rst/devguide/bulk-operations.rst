===============
Bulk operations
===============

This chapter describes bulk operations that are available with Cloud
Files.

Extracting archive files
------------------------

An extract archive request expands tar files into a Cloud Files account.
The request is a **PUT** operation with the ``?extract-archive=format``
query parameter specifying the format of the archive file.

Valid values for the ``format`` variable are ``tar``, ``tar.gz``, and
``tar.bz2``.

.. note::
   This bulk operation involves middleware that conducts many operations
   on a single request.

For the **PUT** request, use the following URI:

/``v1/AUTH_Account/$UPLOAD_PATH?extract-archive=tar.gz``

``UPLOAD_PATH`` is the location where the files are expanded and can
specify any of the following values:

-  A container

-  A pseudo directory within a container

-  An empty string

   If the ``UPLOAD_PATH`` is an empty string, Cloud Files automatically
   creates containers in which to place the files. Files in the base
   directory of the tar file (that is, files that are not in a folder of
   the unzipped tar file) are ignored.

The destination of a file in the archive is built as follows:

``/v1/AUTH_Account/$UPLOAD_PATH/$FILE_PATH``

``FILE_PATH`` is the file name from the listing in the tar file.

The following example shows a request to extract an archive.

**Example: Example extract archive request**

.. code::

    $ tar cf archive.tar directory_to_be_archived
    $ curl -i -XPUT -H'x-auth-token: AUTH_TOKEN'
    https://storage101.iad3.clouddrive.com/v1/MossoCloudFS_aaa-aaa-aaa-aaa?extract-archive=tar -T ./archive.tar

You can create up to 1,000 new containers per extraction request. Also
note that only regular files are uploaded. Objects such as empty
directories and symlinks are not uploaded.

The responses from bulk operations are not like other Cloud Files
responses because a short request body sent from the client could result
in many operations on the proxy server and precautions need to be taken
to prevent the request from timing out because of a lack of activity. To
this end, the client always receives a 200 OK response, regardless of
the actual success of the call. The body of the response, which can be
delivered over a greater amount of time, must be parsed to determine the
actual success of the operation. In addition, the client might receive
whitespace characters prepended to the response body while the proxy
server is completing the request.

The format of the response body defaults to text plain but can be either
JSON or XML depending on the ``Accept`` header. Acceptable formats are
``text/plain``, ``application/json``, ``application/xml``, and
``text/xml``. The following example shows the response body, formatted
in JSON, from a successful request.

**Example: Successful extract archive response**

.. code::

    HTTP/1.1 100 Continue

    HTTP/1.1 200 OK
    Content-Type: application/json
    X-Trans-Id: txa7fd1603cfe04bdb920cd-005191226d
    Date: Mon, 13 May 2013 17:27:10 GMT
    Transfer-Encoding: chunked

    {
      "Number Files Created": 10,
      "Response Status": "201 Created",
      "Errors": [],
      "Response Body": ""
    }

The following example shows a response with errors.

**Example: Extract archive response with errors**

.. code::

    HTTP/1.1 100 Continue

    HTTP/1.1 200 OK
    Content-Type: application/json
    X-Trans-Id: tx9f12e16f047049cc91147-005191245f
    Date:  Mon, 13 May 2013 17:35:27 GMT
    Transfer-Encoding: chunked

    {
      "Number Files Created": 10,
      "Response Status": "400 Bad Request",
      "Errors": [
        [
          "/v1/AUTH_test/test_cont/big_file.wav",
          "413 Request Entity Too Large"
        ]
      ],
      "Response Body": ""
    }

Errors are presented as a list of tuples in the form
``[objectPath, errorResponse]``. The ``objectPath`` given is
the full path where the object was to be put. The ``errorResponse`` is
the HTTP status of the response for that individual **PUT** operation.
After 1,000 errors, processing of the request ends, and the completed
response is returned.

If all valid files were uploaded successfully, the ``Response Status``
in the response body is 201 Created. If any files failed to be created,
the ``Response Status`` corresponds to the subrequest's error.
Possible codes are 400, 401, and 502. In both cases, the
``Response Body`` specifies the number of files successfully uploaded
and a list of the files that failed. (The actual HTTP status code is
always 200 OK, so the ``Response Status`` in the response body is the
one you should monitor.)

.. note::
   If you send a ``Content-Type`` header on the **PUT** request, the
   specified ``Content-Type`` applies to every object in the archive. If
   you set ``Content-Type`` to a blank string, Cloud Files determines the
   ``Content-Type`` based on the individual file type. For example, if you
   have Multipurpose Internet Mail Extensions (MIME) type files, use a
   blank string for ``Content-Type`` to set the MIME type for files within
   the archive.
