.. _cf-dg-large-objects:

======================
Creating large objects
======================

The content of an object cannot be larger than 5 GB, by default.
However, you can store a larger amount of content by using the following
types of objects:

-  Segment objects: You divide your content into pieces and upload each
   piece into its own object, which is a segment object.

-  Manifest objects: You create a manifest object that "points to" the
   segment objects.

Segment objects do not have any special features and can be created,
updated, downloaded, and deleted. However, a manifest object is
special—when you download, the system concatenates the contents of the
segment objects and returns the concatenation in the response body of
the request. This behavior extends to the response headers returned by
**GET** and **HEAD** operations. The value of the ``Content-Length``
header is the total size of all segment objects, and the value of the
``ETag`` header is calculated by taking the ``ETag`` value of each
segment, concatenating them together, and then returning the MD5
checksum of the result.

.. note::
   If you use a manifest object as the source in a **COPY** operation,
   the new object is a "normal" object (not segmented). If the total size of
   the source segment objects exceeds 5 GB, the **COPY** operation fails.
   However, you can make a duplicate of the manifest object. This new
   object can be larger than 5 GB.

Following are the types of manifest objects:

-  Dynamic large objects: The manifest object has no content. However,
   it has the ``X-Object-Manifest`` metadata header. The value of this
   header is ``container``/``prefix``, where ``container`` is the
   name of the container where the segment objects are stored and
   ``prefix`` is a string that all the segment objects have in common.

-  Static large objects: The manifest object content is an ordered list
   of the names of the segment objects in JSON format.

Although both types of manifest objects have similar behavior, there are
differences as explained in the following table.

**Table: Comparison of static and dynamic large objects**

+-------------------------+--------------------------+-------------------------+
| Feature                 | Static large object      | Dynamic large object    |
+=========================+==========================+=========================+
| End-to-end integrity    | Assured. The list of     | Not assured. The        |
|                         | segments includes the    | eventual consistency    |
|                         | MD5 checksum (ETag) of   | model means that        |
|                         | each segment. You cannot | although you have       |
|                         | upload the manifest      | uploaded a segment      |
|                         | object if the ETag in    | object, it might not    |
|                         | the list differs from    | appear in the container |
|                         | the segment object       | list immediately. If    |
|                         | already uploaded. If a   | you download the        |
|                         | segment is somehow lost, | manifest before the     |
|                         | an attempt to download   | object appears in the   |
|                         | the manifest object      | container, the object   |
|                         | results in an error.     | will not be part of the |
|                         |                          | content returned in     |
|                         |                          | response to a **GET**   |
|                         |                          | request.                |
+-------------------------+--------------------------+-------------------------+
| Upload order            | The segment objects must | You can upload manifest |
|                         | be uploaded before the   | and segment objects in  |
|                         | manifest object.         | any order. We recommend |
|                         |                          | that you upload the     |
|                         |                          | manifest object after   |
|                         |                          | the segments in case a  |
|                         |                          | premature download of   |
|                         |                          | the manifest occurs.    |
|                         |                          | However, this is not    |
|                         |                          | enforced.               |
+-------------------------+--------------------------+-------------------------+
| Removal or addition of  | You cannot add or remove | You can upload new      |
| segment objects         | segment objects from the | segment objects or      |
|                         | manifest. However, you   | remove existing         |
|                         | can create a completely  | segments—the names must |
|                         | new manifest object of   | simply match the        |
|                         | the same name with a     | ``<prefix>`` supplied   |
|                         | different manifest list. | in the                  |
|                         |                          | ``X-Object-Manifest``   |
|                         |                          | header.                 |
+-------------------------+--------------------------+-------------------------+
| Segment object size and | Segment objects must be  | Segment objects can be  |
| number                  | at least 1 MB in size,   | of any size.            |
|                         | by default. The final    |                         |
|                         | segment object can be    |                         |
|                         | any size. By default, a  |                         |
|                         | maximum of 1000 segments |                         |
|                         | are supported.           |                         |
+-------------------------+--------------------------+-------------------------+
| Segment object          | The manifest list        | All segment objects     |
| container name          | includes the container   | must be in the same     |
|                         | name of each object      | container.              |
|                         | (that is, segment        |                         |
|                         | objects might be in      |                         |
|                         | different containers).   |                         |
+-------------------------+--------------------------+-------------------------+
| Manifest object         | The object has the       | The                     |
| metadata                | ``X-Static-Large-Object``| ``X-Object-Manifest``   |
|                         |                          | header value is         |
|                         | metadata header set to   | ``container``/``prefix``|
|                         | ``True``. You do not set |                         |
|                         | this metadata directly.  | indicating where the    |
|                         | Instead the system sets  | segment objects are     |
|                         | it when you use a        | located. You supply     |
|                         | **PUT** operation on a   | this request header in  |
|                         | static manifest object.  | the **PUT** operation.  |
+-------------------------+--------------------------+-------------------------+
| Making a copy of the    | To make a copy of the    | The **COPY** operation  |
| manifest object         | manifest object, include | does not create a       |
|                         | the                      | manifest object. To     |
|                         | ?multipart-manifest=get  | duplicate a manifest    |
|                         | query string with the    | object, use the **GET** |
|                         | **COPY** operation. The  | operation to read the   |
|                         | new object contains the  | value of                |
|                         | same manifest as the     | ``X-Object-Manifest``   |
|                         | original. The segment    | and use this value in   |
|                         | objects are not copied.  | the                     |
|                         | Instead, both the        | ``X-Object-Manifest``   |
|                         | original and new         | request header in a     |
|                         | manifest objects share   | **PUT** operation. This |
|                         | the same set of segment  | creates a new manifest  |
|                         | objects.                 | object that shares the  |
|                         |                          | same set of segment     |
|                         |                          | objects as the original |
|                         |                          | manifest object.        |
+-------------------------+--------------------------+-------------------------+

Creating a dynamic large object
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Objects that are larger than 5 GB must be segmented into smaller segment
objects before you upload them. You then upload the segment objects as
you would any other object. You create a manifest object that tells
Cloud Files how to find the segments that make up the large object. The
segments remain individually addressable, but retrieving the manifest
object streams all the segments, concatenated. There is no limit to the
number of segments that can be a part of a single large object. Dynamic
large objects rely on the eventual consistency model.

.. note::
   In this context, the eventual consistency model means that although
   you have uploaded a segment object, it might not appear in the container
   list immediately. If you download the manifest before the segment object
   appears in the container, the object will not be part of the content
   returned in response to a **GET** request.

To ensure that the download works correctly, you must upload all the
object segments to the same container and ensure that each object name
is prefixed in such a way that the names sort in the order in which they
should be concatenated. You also create and upload a manifest file. The
manifest file is simply a zero-byte file with the extra
``X-Object-Manifest: container``/``prefix`` header,
where ``container`` is the container that the object segments are in and
``prefix`` is the common prefix for all the segments. The container and
common prefix must be UTF-8 encoded and URL-encoded in the
``X-Object-Manifest`` header.

It is best to upload all the segments first and then create or update
the manifest. With this method, the full object will not be available
for downloading until the upload is complete. Also, you can upload a new
set of segments to a second location and then update the manifest to
point to this new location. During the upload of the new segments, the
original manifest will still be available to download the first set of
segments.

.. note::
   The segments are deletable by the user at any time. If a segment is
   deleted by mistake, a dynamic large object, having no way of knowing the
   segment was ever there, ignores the deleted file, and the user is
   returned an incomplete file.

The following examples show how to upload a segment of a large object,
the next segment of a large object, and the manifest.

**Example: Upload a segment of a large object: HTTP request**

.. code::

    PUT /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer/MyObject HTTP/1.1
    Host: storage.clouddrive.com
    X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c
    ETag: 8a964ee2a5e88be344f36c22562a6486
    Content-Length: 1

**Example: Upload a segment of a large object response**

.. code::

    s

No response body is returned. A status code of 201 (Created) indicates a
successful write. Status code 411 (Length Required) indicates that the
``Content-Length`` header is missing. If the MD5 checksum calculated by
the storage system does not match the optionally supplied ``ETag`` value, a
422 (Unprocessable Entity) status code is returned.

You can continue uploading segments as this example shows, prior to
uploading the manifest.

**Example: Upload the next segment of the large object : HTTP
request**

.. code::

    PUT /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer/MyObject HTTP/1.1
    Host: storage.clouddrive.com
    X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c
    ETag: 8a964ee2a5e88be344f36c22562a6486
    Content-Length: 1

**Example: Upload the next segment of the large object response**

.. code::

    w

Next, upload the manifest that you created that indicates the container
in which the object segments reside. Note that uploading additional
segments after the manifest is created causes the concatenated object to
be that much larger, but you do not need to re-create the manifest file
for subsequent additional segments.

**Example: Upload manifest: HTTP request**

.. code::

    PUT /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer/MyObject HTTP/1.1
    Host: storage.clouddrive.com
    X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c
    Content-Length: 0
    X-Object-Manifest: container/prefix/object/segments

**Example: Upload manifest response**

.. code::

    [...]

A **GET** request to the manifest object returns the concatenation of
the objects from the manifest.

When you perform a **GET** or **HEAD** request on the manifest, the
response's ``Content-Type`` is the same as the ``Content-Type`` that was
set during the **PUT** request that created the manifest. You can easily
change the ``Content-Type`` by reissuing the **PUT** request.

.. note::
   The ``ETag`` in the response for a **GET** or **HEAD** on the manifest
   file is the MD5 sum of the concatenated string of ETags for each of the
   segments in the manifest. Usually, the ``ETag`` is the MD5 sum of the
   contents of the object, and that holds true for each segment
   independently. But it is not meaningful to generate such an ETag for the
   manifest itself, so this method was chosen to at least offer change
   detection.

Creating a static large object
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Static large object (SLO) support is similar to dynamic large object
(DLO) support because it enables you to upload many objects concurrently
and later download them as a single object. However, unlike dynamic
large object support, static large object support does not rely on the
eventual consistency model for the container listings. Instead, static
large object support uses a user-defined manifest of the object
segments.

The benefits of using static large objects are as follows:

-  The objects that are uploaded and downloaded can be in different
   containers, which can improve performance.

-  There is an explicit list of segments, instead of an implied list as
   with dynamic large objects.

You create a static large object by performing the following steps:

#. Divide your content into pieces and create (upload) a segment object
   to contain each piece. You must record the ``ETag`` response header
   returned by the **PUT** operation. Alternatively, you can calculate
   the MD5 checksum of the segment prior to uploading and include this
   in the ``ETag`` request header. Doing so ensures that the upload
   cannot corrupt your data. For detailed information, see the section
   called “Uploading the segments” .

   The maximum number of segment objects per static large object is
   1,000. Each segment, except for the final one, must be at least 1 MB.

#. Create a manifest object by listing the name of each segment object
   along with its size and MD5 checksum, in order. You indicate that
   this is a manifest object by including the
   ?\ ``multipart-manifest=put`` query string at the end of the manifest
   object name. For detailed information, see the section called
   “Uploading the manifest”.


Uploading the segments
^^^^^^^^^^^^^^^^^^^^^^

Upload your segment objects. All the segments, except the last one, need
to be larger than 1 MB (1048576 bytes). It might help organizationally
to keep them in the same container, but it is not required. You need the
following information about each segment for the next step, uploading
the manifest object:

-  ``path`` – The container and object name in the following format:
   ``containerName``/*``objectName``*

-  ``etag`` – The ``ETag`` header from the successful 201 response of
   the **PUT** operation that uploaded the segment. This is the MD5
   checksum of the segment object's data.

-  ``size_bytes`` – The segment object's size in bytes. This value must
   match the ``Content-Length`` of that object.

Uploading the manifest
^^^^^^^^^^^^^^^^^^^^^^

After you have uploaded the objects to be concatenated, you upload a
manifest object. The request must use the **PUT** operation, with the
following query parameter at the end of the manifest object name:

.. code::

    ?multipart-manifest=put

The body of the **PUT** operation is an ordered list of files in JSON
data format. The data to be supplied for each segment is as follows:

-  ``path`` – The container and object name in the following format:
   ``containerName``/*``objectName``*

-  ``etag`` – The ``ETag`` header from the successful 201 response of
   the **PUT** operation that uploaded the segment. This is the MD5
   checksum of the segment object's data.

-  ``size_bytes`` – The segment object's size in bytes. This value must
   match the ``Content-Length`` of that object.

Following is an example containing three segment objects. This example
illustrates that in contrast to dynamic large objects, you can use a
number of containers and the object names do not have to conform to a
specific pattern.

**Example: Static large object manifest list**

.. code::

    [
            {
              "path": "/mycontainer/objseg1",
              "etag": "0228c7926b8b642dfb29554cd1f00963",
              "size_bytes": 1468006
            },
            {
              "path": "/mycontainer/pseudodir/seg-obj2",
              "etag": "5bfc9ea51a00b790717eeb934fb77b9b",
              "size_bytes": 1572864
            },
            {
              "path": "/other-container/seg-final",
              "etag": "b9c3da507d2557c1ddc51f27c54bae51",
              "size_bytes": 256
            }
    ]

The ``Content-Length`` request header must contain the length of the
JSON content, not the length of the segment objects. However, after the
**PUT** operation is complete, the ``Content-Length`` metadata is set to
the total length of all the object segments. A similar situation applies
to the ``ETag`` header. If it is used in the **PUT** operation, it must
contain the MD5 checksum of the JSON content. The ``ETag`` metadata
value is then set to be the MD5 checksum of the concatenated ``ETag``
values of the object segments. You can also set the ``Content-Type``
request header and custom object metadata.

When the **PUT** operation sees the ``?multipart-manifest=put`` query
string, it reads the request body and verifies that each segment object
exists and that the sizes and ETags match. If there is a mismatch, the
**PUT** operation fails.

When you upload the manifest object, the middleware reads every segment
passed in and verifies the size and ETag of each. If any of the objects
do not match (for example, an object is not found, the size or ``ETag``
is mismatched, or the minimum size is not met), or if everything does
match and a manifest object is created, Cloud Files issues a response
code. The response codes are the same as those issued for the create or
update object operation (see “Create or update object”).

When Cloud Files creates the manifest object, Cloud Files sets the
``X-Static-Large-Object`` metadata header to ``True``, indicating that
this is a static object manifest.

When the manifest object is uploaded, you can be generally assured that
every segment in the manifest exists and that it matches the
specifications. However, nothing prevents a user from breaking the
static large object download by deleting or replacing a segment that is
referenced in the manifest. Users should use caution when handling the
segments.

The order of the segments listed in the manifest determines the order in
which the segments are concatenated when downloaded. The manifest can
reference objects in separate containers, which improves concurrent
upload speed. A single object can be referenced by multiple manifests.

Retrieving a large object
^^^^^^^^^^^^^^^^^^^^^^^^^

A **GET** request to the manifest object returns the concatenated
content of the segment objects listed in the manifest. If any of the
segments from the manifest are not found or their ``ETag`` or
``Content-Length`` values no longer match, the **GET** operation fails
and you receive partial results (up to the point of the failure due to
not matching). As a result, a 409 (Conflict) status code is logged.

The headers from the **GET** or **HEAD** request return metadata for the
manifest object as follows:

-  ``Content-Length``: The total size of the static large object (the
   sum of the sizes of the segments in the manifest)

-  ``X-Static-Large-Object: True``

-  ``ETag``: The ETag of the static large object (generated the same way
   as a dynamic large object)

The **GET** request with the following query parameter returns the actual
manifest file contents:

.. code::

    ?multipart-manifest=get  

The response body contains generated JSON. The resulting list is not
identically formatted like the manifest that you originally used in the
**PUT** operation (``?multipart-manifest=put``).

The main purpose of the **GET** or **HEAD** operation is for debugging.

Deleting a large object
^^^^^^^^^^^^^^^^^^^^^^^

A **DELETE** operation on a manifest object deletes the manifest object
itself. The segment objects are not affected.

A **DELETE** operation with the following query parameter deletes all
segment objects in the manifest, and then, if all are successfully
deleted, the manifest object itself. A failure response is similar to
those for the bulk delete operation (:ref:`Bulk delete<cf-dg-bulk-delete>`).

.. code::

    ?multipart-manifest=delete

Modifying a large object
^^^^^^^^^^^^^^^^^^^^^^^^

**PUT** and **POST** operations work as follows:

-  A **PUT** operation overwrites the manifest object (and leaves the
   segments alone).

-  A **POST** operation changes the manifest file's metadata and
   contents, as with any other object.

Listing containers with static large objects
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In a list of containers, the size listed for a static large object
manifest object is the total size of the concatenated segments in the
manifest, not the size of the manifest file itself. The overall
``X-Container-Bytes-Used`` for the container (and for the account) does
not reflect the total size of the manifest, but the actual size of the
stored JSON data. This enables you to see the total size of the static
large object in a container list, but does not inflate the bytes used
for the container or the account.

