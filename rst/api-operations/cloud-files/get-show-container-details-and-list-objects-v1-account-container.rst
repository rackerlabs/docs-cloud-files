
.. THIS OUTPUT IS GENERATED FROM THE WADL. DO NOT EDIT.

=============================================================================
Show Container Details And List Objects -  Rackspace Cloud Files™ Developer Guide
=============================================================================

Show Container Details And List Objects
~~~~~~~~~~~~~~~~~~~~~~~~~

`Request <get-show-container-details-and-list-objects-v1-account-container.html#request>`__
`Response <get-show-container-details-and-list-objects-v1-account-container.html#response>`__

.. code::

    GET /v1/{account}/{container}

Shows details for a specified container and lists objects, sorted by name, in the container.

This operation against a storage container name retrieves a list of the objects stored in the container. You can use optional query parameters to refine the list results.

A request with no query parameters returns the full list of object names stored in the container, up to 10,000 names. The response body shows the object names as one object name per line. Specifying the query parameters filters the full list and returns a subset of objects. For information about limiting and controlling the list, see the following “Controlling a Large List of Objects” section.

An HTTP response status code of 200 through 299 indicates success. A status code of 200 (OK) is returned if there are objects, and a 204 (No Content) is returned if there are no objects. If the container does not exist, or if an incorrect account is specified, a status code 404 (Not Found) is returned.

Format Object List

If you append the ``format=xml`` or the ``format=json`` query parameter to the storage account URL, the service returns additional object information serialized in the specified format. The status codes are the same for ``format=xml`` and ``format=json``. However, ``Content-Type`` matches the specified format. The example responses in this section are formatted for readability.

Controlling a Large List of Objects

A ``GET`` request against the container account URL returns a list of up to 10,000 objects. You can limit and control this list of results by using the ``marker``, ``end_marker``, and ``limit`` parameters.

The ``marker`` parameter tells Cloud Files where to begin your list of objects, and the ``end_marker`` parameter tells where to end the list. You can use them either independently or together, separated by an ampersand ( ``&`` ). If you do not specify them, your list displays up to 10,000 objects. Note that the ``marker`` and ``end_marker`` values must be URL-encoded before you send the HTTP request.

You can use the ``limit`` parameter to reduce the number of returned objects.

If the number of returned items equals the ``limit`` used (or 10,000 if no ``limit`` was specified), you can assume there are more object names.

As an example, use a listing of 5 object names, as follows:

gala grannysmith honeycrisp jonagold reddelicious

Use a ``limit`` of 2 to show how things work:

GET /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/AppleType?limit=2 Host: storage.clouddrive.com X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c gala grannysmith

Because the request returned two items, assume there are more object names to list and make another request with a ``marker`` of the last item returned:

GET /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/AppleType?limit=2&marker=grannysmith Host: storage.clouddrive.com X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c honeycrisp jonagold

Again, two items are returned, and you assume that there might be more. So you make another ``GET`` request for two more:

GET /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/AppleType?limit=2&marker=jonagold Host: storage.clouddrive.com X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c reddelicious

This one-item response shows fewer than the limit of two object names requested, and indicates that this is the end of the list.



This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |OK                       |The request succeeded.   |
|                          |                         |The information returned |
|                          |                         |with the response is     |
|                          |                         |dependent on the method  |
|                          |                         |used in the request.The  |
|                          |                         |length of the response   |
|                          |                         |body that contains the   |
|                          |                         |list of names. If the    |
|                          |                         |operation fails, this    |
|                          |                         |value is the length of   |
|                          |                         |the error text in the    |
|                          |                         |response body.The number |
|                          |                         |of objects.The type of   |
|                          |                         |ranges that the object   |
|                          |                         |accepts.The count of     |
|                          |                         |bytes used in total.The  |
|                          |                         |custom container         |
|                          |                         |metadata item,           |
|                          |                         |where``name`` is the     |
|                          |                         |name of the metadata     |
|                          |                         |item. One ``X-Container- |
|                          |                         |Meta-name`` response     |
|                          |                         |header appears for each  |
|                          |                         |metadata item (for       |
|                          |                         |each``name``).The MIME   |
|                          |                         |type of the list of      |
|                          |                         |names. If the operation  |
|                          |                         |fails, this value is the |
|                          |                         |MIME type of the error   |
|                          |                         |text in the response     |
|                          |                         |body.A unique            |
|                          |                         |transaction identifier   |
|                          |                         |for this request.The     |
|                          |                         |transaction date and     |
|                          |                         |time.                    |
+--------------------------+-------------------------+-------------------------+
|204                       |No Content               |The request succeeded.   |
|                          |                         |The server fulfilled the |
|                          |                         |request but does not     |
|                          |                         |need to return a body.   |
+--------------------------+-------------------------+-------------------------+
|404                       |Not Found                |The requested resource   |
|                          |                         |was not found.           |
+--------------------------+-------------------------+-------------------------+
|409                       |Conflict                 |The request could not be |
|                          |                         |completed due to a       |
|                          |                         |conflict with the        |
|                          |                         |current state of the     |
|                          |                         |resource.                |
+--------------------------+-------------------------+-------------------------+


Request
^^^^^^^^^^^^^^^^^

This table shows the URI parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|{account}                 |xsd:string               |Your unique account      |
|                          |                         |identifier.              |
+--------------------------+-------------------------+-------------------------+
|{container}               |xsd:string               |The unique identifier of |
|                          |                         |the container.           |
+--------------------------+-------------------------+-------------------------+



This table shows the query parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|limit                     |xsd:int *(Required)*     |For an integer n, limits |
|                          |                         |the number of results to |
|                          |                         |n values.                |
+--------------------------+-------------------------+-------------------------+
|marker                    |xsd:string *(Required)*  |Given a string value x,  |
|                          |                         |returns object names     |
|                          |                         |greater in value than    |
|                          |                         |the specified marker.    |
+--------------------------+-------------------------+-------------------------+
|end_marker                |xsd:string *(Required)*  |Given a string value x,  |
|                          |                         |returns object names     |
|                          |                         |lesser in value than the |
|                          |                         |specified marker.        |
+--------------------------+-------------------------+-------------------------+
|prefix                    |xsd:string *(Required)*  |For a string value x,    |
|                          |                         |causes the results to be |
|                          |                         |limited to object names  |
|                          |                         |beginning with the       |
|                          |                         |substring x.             |
+--------------------------+-------------------------+-------------------------+
|format                    |xsd:string *(Required)*  |Specifies either JSON or |
|                          |                         |XML to return the        |
|                          |                         |respective serialized    |
|                          |                         |response.                |
+--------------------------+-------------------------+-------------------------+
|delimiter                 |xsd:char *(Required)*    |For a character c,       |
|                          |                         |returns the object names |
|                          |                         |nested in the container  |
|                          |                         |(without the need for    |
|                          |                         |the directory marker     |
|                          |                         |objects).                |
+--------------------------+-------------------------+-------------------------+
|path                      |xsd:string *(Required)*  |For a string x, returns  |
|                          |                         |the object names nested  |
|                          |                         |in the pseudo path. This |
|                          |                         |parameter is equivalent  |
|                          |                         |to setting the delimiter |
|                          |                         |parameter to / and the   |
|                          |                         |prefix to the path with  |
|                          |                         |a / on the end. For more |
|                          |                         |information about pseudo |
|                          |                         |paths, see the section   |
|                          |                         |on pseudo hierarchical   |
|                          |                         |folders and directories. |
+--------------------------+-------------------------+-------------------------+







**Example Show Container Details And List Objects: XML request**


.. code::

    GET /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer?
    format=xml HTTP/1.1
    Host: storage.clouddrive.com
    X-Storage-Token: 182f9c0af0e828cfe3281767d29d19f4


**Example Show Container Details And List Objects: JSON request**


.. code::

    GET /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer?
    format=json HTTP/1.1
    Host: storage.clouddrive.com
    X-Storage-Token: 182f9c0af0e828cfe3281767d29d19f4


Response
^^^^^^^^^^^^^^^^^^





**Example Show Container Details And List Objects: XML response**


.. code::

    HTTP/1.1 200 OK
    Content-Length: 500
    X-Container-Object-Count: 2
    Accept-Ranges: bytes
    X-Container-Meta-Book: TomSawyer
    X-Timestamp: 1389727543.65372
    X-Container-Bytes-Used: 26
    Content-Type: application/xml; charset=utf-8
    X-Trans-Id: txc75ea9a6e66f47d79e0c5-0052d6be76
    Date: Wed, 15 Jan 2014 16:59:35 GMT
    
    <?xml version="1.0" encoding="UTF-8"?>
    <container name="marktwain">
        <object>
            <name>goodbye</name>
            <hash>451e372e48e0f6b1114fa0724aa79fa1</hash>
            <bytes>14</bytes>
            <content_type>application/octet-stream</content_type>
            <last_modified>2014-01-15T16:41:49.390270</last_modified>
        </object>
        <object>
            <name>helloworld</name>
            <hash>ed076287532e86365e841e92bfc50d8c</hash>
            <bytes>12</bytes>
            <content_type>application/octet-stream</content_type>
            <last_modified>2014-01-15T16:37:43.427570</last_modified>
        </object>
    </container>


**Example Show Container Details And List Objects: JSON response**


.. code::

    HTTP/1.1 200 OK
    Content-Length: 341
    X-Container-Object-Count: 2
    Accept-Ranges: bytes
    X-Container-Meta-Book: TomSawyer
    X-Timestamp: 1389727543.65372
    X-Container-Bytes-Used: 26
    Content-Type: application/json; charset=utf-8
    X-Trans-Id: tx26377fe5fab74869825d1-0052d6bdff
    Date: Wed, 15 Jan 2014 16:57:35 GMT
    
    [
     {
     "hash":"451e372e48e0f6b1114fa0724aa79fa1",
     "last_modified":"2014-01-15T16:41:49.390270",
     "bytes":14,
     "name":"goodbye",
     "content_type":"application/octet-stream"
     },
     {
     "hash":"ed076287532e86365e841e92bfc50d8c",
     "last_modified":"2014-01-15T16:37:43.427570",
     "bytes":12,
     "name":"helloworld",
     "content_type":"application/octet-stream"
     }
    ]

