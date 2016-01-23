
.. THIS OUTPUT IS GENERATED FROM THE WADL. DO NOT EDIT.

.. _show-object-metadata:

Show object metadata
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    HEAD /v1/{account}/{container}/{object}


This operation performs a HEAD operation on an object to retrieve object metadata and other standard HTTP headers.

This operation does not return a response body. Metadata is returned as HTTP headers.

.. note::
   The ``HEAD`` return code for an object is different than the ``HEAD`` return code for a container. A ``HEAD`` request does not return a message body in the response, so a status code of 200 through 299 indicates success. When a ``HEAD`` request is performed against a container, it queries the container databases, and it does not retrieve the content from them. Thus, this operation returns the 204 (No Content) status code. However, when a ``HEAD`` request is performed against an object, it returns a 200 OK status code because it can view the content. 
   
   



This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |OK                       |The request has          |
|                          |                         |succeeded.               |
+--------------------------+-------------------------+-------------------------+
|404                       |Not Found                |The requested resource   |
|                          |                         |was not found.           |
+--------------------------+-------------------------+-------------------------+


Request
""""""""""""""""


This table shows the header parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|X-Auth-Token              |String *(Required)*      |Authentication token.    |
+--------------------------+-------------------------+-------------------------+




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
|                |                |temporary URLs, see :ref:`TempURL<tempurl>`.|
+----------------+----------------+--------------------------------------------+
|expires         |String          |Used with temporary URLs to specify the     |
|                |*(Optional)*    |expiry time of the signature. For more      |
|                |                |information about temporary URLs, see       |
|                |                |:ref:`TempURL<tempurl>`.                    |
+----------------+----------------+--------------------------------------------+




This operation does not accept a request body.




**Example Get object metadata: HTTP request**


.. code::

   HEAD /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer/MyObject HTTP/1.1
   Host: storage.clouddrive.com
   X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c





Response
""""""""""""""""


This table shows the header parameters for the response:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|X-Timestamp               |String *(Required)*      |An internal variable     |
|                          |                         |that indicates the last  |
|                          |                         |time an entity (account, |
|                          |                         |container, or object)    |
|                          |                         |was modified. The format |
|                          |                         |is the same as a Unix    |
|                          |                         |timestamp. The storage   |
|                          |                         |system uses this header  |
|                          |                         |to determine the latest  |
|                          |                         |version. For example,    |
|                          |                         |during replication, the  |
|                          |                         |storage system makes     |
|                          |                         |sure all three object    |
|                          |                         |replicas are up to date, |
|                          |                         |and it uses the X-       |
|                          |                         |Timestamp header to      |
|                          |                         |determine which replica  |
|                          |                         |is the latest. You might |
|                          |                         |notice that objects have |
|                          |                         |both a Last-Modified and |
|                          |                         |X-Timestamp header. The  |
|                          |                         |difference between these |
|                          |                         |two headers is the       |
|                          |                         |resolution. Last-        |
|                          |                         |Modified has resolution  |
|                          |                         |up to one second, while  |
|                          |                         |X-Timestamp has          |
|                          |                         |resolution up to five    |
|                          |                         |decimal places of one    |
|                          |                         |second.                  |
+--------------------------+-------------------------+-------------------------+
|Last-Modified             |String *(Required)*      |An internal variable     |
|                          |                         |that indicates the last  |
|                          |                         |time an entity (account, |
|                          |                         |container, or object)    |
|                          |                         |was modified. For Last-  |
|                          |                         |Modified, the time zone  |
|                          |                         |is UTC. You might notice |
|                          |                         |that objects have both a |
|                          |                         |Last-Modified and X-     |
|                          |                         |Timestamp header. The    |
|                          |                         |difference between these |
|                          |                         |two headers is the       |
|                          |                         |resolution. Last-        |
|                          |                         |Modified has resolution  |
|                          |                         |up to one second, while  |
|                          |                         |X-Timestamp has          |
|                          |                         |resolution up to five    |
|                          |                         |decimal places of one    |
|                          |                         |second.                  |
+--------------------------+-------------------------+-------------------------+
|Content-Length            |String *(Required)*      |The length of the object |
|                          |                         |content in the response  |
|                          |                         |body, in bytes.          |
+--------------------------+-------------------------+-------------------------+
|Etag                      |String *(Required)*      |The MD5 checksum of the  |
|                          |                         |uploaded object content. |
|                          |                         |The value is not quoted. |
+--------------------------+-------------------------+-------------------------+
|Content-Type              |String *(Required)*      |The MIME type of the     |
|                          |                         |object.                  |
+--------------------------+-------------------------+-------------------------+
|X-Trans-Id                |Uuid *(Required)*        |A unique transaction     |
|                          |                         |identifier for this      |
|                          |                         |request.                 |
+--------------------------+-------------------------+-------------------------+
|Date                      |Datetime *(Required)*    |The transaction date and |
|                          |                         |time.                    |
+--------------------------+-------------------------+-------------------------+
|Content-Encoding          |String *(Optional)*      |If set, the value of the |
|                          |                         |``Content-Encoding``     |
|                          |                         |metadata. If not set,    |
|                          |                         |this header is not       |
|                          |                         |returned by this         |
|                          |                         |operation.               |
+--------------------------+-------------------------+-------------------------+
|Content-Disposition       |String *(Optional)*      |If set, specifies the    |
|                          |                         |override behavior for    |
|                          |                         |the browser. For         |
|                          |                         |example, this header     |
|                          |                         |might specify that the   |
|                          |                         |browser use a download   |
|                          |                         |program to save this     |
|                          |                         |file rather than show    |
|                          |                         |the file, which is the   |
|                          |                         |default. If not set,     |
|                          |                         |this header is not       |
|                          |                         |returned by this         |
|                          |                         |operation.               |
+--------------------------+-------------------------+-------------------------+
|X-Delete-At               |String *(Optional)*      |If set, the time when    |
|                          |                         |the object will be       |
|                          |                         |deleted by the system in |
|                          |                         |the format of a UNIX     |
|                          |                         |epoch timestamp. If not  |
|                          |                         |set, this header is not  |
|                          |                         |returned by this         |
|                          |                         |operation.               |
+--------------------------+-------------------------+-------------------------+
|X-Object-Manifest         |String *(Optional)*      |If set, to this is a     |
|                          |                         |dynamic large object     |
|                          |                         |manifest object. The     |
|                          |                         |value is the container   |
|                          |                         |and object name prefix   |
|                          |                         |of the segment objects   |
|                          |                         |in the form              |
|                          |                         |``container/prefix``.    |
+--------------------------+-------------------------+-------------------------+
|X-Static-Large-Object     |Boolean *(Optional)*     |Set to ``True`` if this  |
|                          |                         |object is a static large |
|                          |                         |object manifest object.  |
+--------------------------+-------------------------+-------------------------+
|X-Object-Meta-name        |String *(Required)*      |The custom object        |
|                          |                         |metadata item, where     |
|                          |                         |``name`` is the name of  |
|                          |                         |the metadata item. One   |
|                          |                         |``X-Object-Meta-name``   |
|                          |                         |response header appears  |
|                          |                         |for each metadata item   |
|                          |                         |(for each ``name``).     |
+--------------------------+-------------------------+-------------------------+




This operation does not return a response body.






**Example Get object metadata: HTTP response**


.. code::

   HTTP/1.1 200 OK
   Date: Thu, 10 Jun 2010 20:59:39 GMT
   Last-Modified: Fri, 11 Jun 2010 13:40:18 GMT
   ETag: 8a964ee2a5e88be344f36c22562a6486
   Content-Length: 512000
   Content-Type: text/plain; charset=UTF-8
   X-Object-Meta-Meat: Bacon
   X-Object-Meta-Fruit: Apple
   X-Object-Meta-Veggie: Beans
   X-Object-Meta-Dairy: Cheese




