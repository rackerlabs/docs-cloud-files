
.. _copy-object:

Copy object
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    COPY /v1/{account}/{container}/{object}

Using the ``Destination`` header, copies an existing object to another object with a new name in the Cloud Files storage system.

The new object can be in the same container, but have a different name from the original object. Or, the new object can have the same or a different name and be located in a different container than the original object.

.. note::
   You can use a ``PUT`` operation with the ``X-Copy-From`` header to accomplish the same operation as the ``COPY`` operation. The ``PUT`` operation always creates a new object. If you use this operation on an existing object, you replace the existing object and metadata rather than modifying the object. 
   
   

Suppose you upload a file with the wrong object name or content type, or you need to move some objects to another container. Without a server-side object copy feature, you would need to repeat uploading the same content and then delete the existing object. With a server-side object copy feature, you can save the step of re-uploading the content and thus also save the associated bandwidth charges, if any were to apply. 

You can send a ``COPY`` request to the existing object and include the ``Destination`` header to specify the destination of the copy. The header value is the container and new object name in the form of ``/container/object``. Unlike using the ``PUT`` request, this approach does not require a ``Content-Length`` header.

**Example: Copy object approach 1 - using COPY**

.. code::
  
   COPY /v1/account/sourceContainer/sourceObject  HTTP/1.1   
   Host: storageURL  
   X-Auth-Token: yourAuthToken   
   Destination: /destinationContainer/destinationObject 

Alternatively, you can send a ``PUT`` request to the location of the new object (the destination), and add the ``X-Copy-From`` header to designate the source of the data. The header value must be the container and object name of the source object in the form of ``/container/object``. The HTTP specification of a ``PUT`` request with the ``X-Copy-From`` header requires a ``Content-Length`` header, but the storage system does not use the ``Content-Length`` value to perform the operation. For this reason, you can simply send a ``Content-Length`` value of 0 (zero). 

.. note::
   By default, you cannot copy an object larger than 5 GB. For information about how to handle objects larger than 5 GB, see :ref:`Authentication <auth>`. 
   
   

**Example: Copy object approach 2 - using PUT**

.. code::
  
   PUT /v1/account/destinationContainer/destinationObject  HTTP/1.1
   Host: storageURL   
   X-Auth-Token: yourAuthToken   
   X-Copy-From: /sourceContainer/sourceObject   
   Content-Length: 0 

With both of these approaches, the destination container must exist before you copy the object.

.. note::
   If you are copying many objects, you can improve the total copy time by issuing several concurrent ``COPY`` commands. Because Cloud Files is a distributed storage system, your concurrent ``COPY`` commands run on separate machines simultaneously. As a best practice, you can run up to 100 concurrent ``COPY`` commands per container. 
   
   

If you want to move the object rather than copy it, send a ``DELETE`` request to the source object after copying it. A move is simply a ``COPY`` operation followed by a ``DELETE`` operation.

All metadata is preserved during the object copy. Note that you can set metadata on the request to copy the object (with either ``PUT`` or ``COPY`` ), and the metadata overwrites any conflicting keys on the destination object. 

Your account is not charged when you copy or move your objects within the same data center by using the internal network URI, ServiceNet, as the storage URL. You can find your ServiceNet endpoint in the service catalog that is created when you authenticate your session. For information about how to authenticate your session, see :ref:`Authentication <auth>`. As shown in the following partial service catalog example, the ServiceNet URI is listed as ``internalURL``. The name is your Cloud Files storage URL with ``snet-`` prepended to it. If you do not know which data center you are working in, you can find it in the Cloud Control Panel. (For more information about service access endpoints, see :ref:`Service access endpoints <service-access>`.)

**Example: Data center endpoints**

.. code::
  
   "endpoints": [     
     {       
       "region": "DFW", 
       "internalURL": "https://snet-storage101.dfw1.clouddrive.com/v1/MossoCloudFS_9491081f-7e12-4f56-98d0-cdb3037c8d7c", 
       "tenantId": "MossoCloudFS_9491081f-7e12-4f56-98d0-cdb3037c8d7c",       
       "publicURL": "https://storage101.dfw1.clouddrive.com/v1/MossoCloudFS_9491081f-7e12-4f56-98d0-cdb3037c8d7c"     
     },     
     {       
       "region": "ORD", 
       "internalURL": "https://snet-storage101.ord1.clouddrive.com/v1/MossoCloudFS_9491081f-7e12-4f56-98d0-cdb3037c8d7c ", 
       "tenantId": "MossoCloudFS_9491081f-7e12-4f56-98d0-cdb3037c8d7c",      
       "publicURL": "https://storage101.ord1.clouddrive.com/v1/MossoCloudFS_9491081f-7e12-4f56-98d0-cdb3037c8d7c"     
     }   
    ] 


This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|201                       |Created                  |The request has been     |
|                          |                         |fulfilled.               |
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



This table shows the header parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|X-Auth-Token              |String *(Required)*      |Authentication token.    |
+--------------------------+-------------------------+-------------------------+
|X-Copy-From               |String                   |Used with PUT, the       |
|                          |                         |container and object     |
|                          |                         |name of the source       |
|                          |                         |object in the form       |
|                          |                         |of ``/container/object``.|
+--------------------------+-------------------------+-------------------------+
|X-Copy-From-Account       |String                   |Specifies the account    |
|                          |                         |you are copying from.    |
+--------------------------+-------------------------+-------------------------+
|Content-Length            |Int *(Required)*         |Used with PUT, the       |
|                          |                         |content length. Zero (0) |
|                          |                         |is always acceptable for |
|                          |                         |this operation.          |
+--------------------------+-------------------------+-------------------------+
|Destination               |String                   |Used with COPY, the      |
|                          |                         |container and object     |
|                          |                         |name of the destination  |
|                          |                         |object in the form       |
|                          |                         |of ``/container/object``.|
+--------------------------+-------------------------+-------------------------+
|Destination-Account       |String                   |Used for account to      |
|                          |                         |account copy. Specifies  |
|                          |                         |the destination account  |
|                          |                         |name (which is the last  |
|                          |                         |part of the storage URL).|
+--------------------------+-------------------------+-------------------------+
|Content-Type              |String                   |The media type of the    |
|                          |                         |entity-body sent. If not |
|                          |                         |specified, the ``Content-|
|                          |                         |Type`` is guessed, by    |
|                          |                         |using the Python         |
|                          |                         |mimetypes library, based |
|                          |                         |on the object path.      |
+--------------------------+-------------------------+-------------------------+
|X-Detect-Content-Type     |String                   |If you set this header   |
|                          |                         |to ``True``, the         |
|                          |                         |``Content-Type`` that is |
|                          |                         |sent in the request (if  |
|                          |                         |any) is ignored, and     |
|                          |                         |``Content-Type`` is      |
|                          |                         |guessed by using the     |
|                          |                         |Python mimetypes library |
|                          |                         |based on the object path.|
+--------------------------+-------------------------+-------------------------+
|Content-Encoding          |String                   |If set, the value of the |
|                          |                         |``Content-Encoding``     |
|                          |                         |metadata.                |
+--------------------------+-------------------------+-------------------------+
|Content-Disposition       |String                   |If set, specifies the    |
|                          |                         |override behavior for    |
|                          |                         |the browser. For         |
|                          |                         |example, this header     |
|                          |                         |might specify that the   |
|                          |                         |browser use a download   |
|                          |                         |program to save this     |
|                          |                         |file rather than show    |
|                          |                         |the file, which is the   |
|                          |                         |default.                 |
+--------------------------+-------------------------+-------------------------+
|X-Object-Meta-name        |String                   |The container metadata,  |
|                          |                         |where ``name`` is the    |
|                          |                         |name of the metadata     |
|                          |                         |item. You must specify a |
|                          |                         |``X-Object-Meta-name``   |
|                          |                         |header for each metadata |
|                          |                         |item (for each ``name``) |
|                          |                         |that you want to add or  |
|                          |                         |update.                  |
+--------------------------+-------------------------+-------------------------+









This operation does not accept a request body.




**Example: Copy object using COPY HTTP request**


.. code::

   COPY /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MySourceContainer/MySourceObject HTTP/1.1
   Host: storage.clouddrive.com
   X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c
   Destination: /MyDestinationContainer/MyDestinationObject





**Example: Copy object using PUT HTTP request**


.. code::

   PUT /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyDestinationContainer/MyDestinationObject HTTP/1.1
   Host: storage.clouddrive.com
   X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c
   X-Copy-From: /MySourceContainer/MySourceObject
   Content-Length: 0    





Response
""""""""""""""""


This table shows the header parameters for the response:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|Content-Length            |String                   |If the operation         |
|                          |                         |succeeds, this value is  |
|                          |                         |zero (0). If the         |
|                          |                         |operation fails, this    |
|                          |                         |value is the length of   |
|                          |                         |the error text in the    |
|                          |                         |response body.           |
+--------------------------+-------------------------+-------------------------+
|Etag                      |String                   |The MD5 checksum of the  |
|                          |                         |uploaded object content. |
|                          |                         |The value is not quoted. |
+--------------------------+-------------------------+-------------------------+
|Content-Type              |String                   |The MIME type of the     |
|                          |                         |object.                  |
+--------------------------+-------------------------+-------------------------+
|X-Trans-Id                |Uuid                     |A unique transaction     |
|                          |                         |identifier for this      |
|                          |                         |request.                 |
+--------------------------+-------------------------+-------------------------+
|Date                      |Datetime                 |The transaction date and |
|                          |                         |time.                    |
+--------------------------+-------------------------+-------------------------+
|X-Copied-From-Last-       |String                   |For a copied object,     |
|Modified                  |                         |shows the last modified  |
|                          |                         |date and time for the    |
|                          |                         |container and object     |
|                          |                         |name from which the new  |
|                          |                         |object was copied.       |
+--------------------------+-------------------------+-------------------------+
|X-Copied-From             |String                   |For a copied object,     |
|                          |                         |shows the container and  |
|                          |                         |object name from which   |
|                          |                         |the new object was       |
|                          |                         |copied. The value is in  |
|                          |                         |form                     |
|                          |                         |``container/object``.    |
+--------------------------+-------------------------+-------------------------+
|Last-Modified             |String                   |The date and time that   |
|                          |                         |the object was created   |
|                          |                         |or the last time that    |
|                          |                         |the metadata was changed.|
+--------------------------+-------------------------+-------------------------+
|X-Object-Meta-name        |String                   |The custom object        |
|                          |                         |metadata item, where     |
|                          |                         |``name`` is the name of  |
|                          |                         |the metadata item. One   |
|                          |                         |``X-Object-Meta-name``   |
|                          |                         |response header appears  |
|                          |                         |for each metadata item   |
|                          |                         |(for each ``name``).     |
+--------------------------+-------------------------+-------------------------+




This operation does not return a response body.





**Example: Copy object using COPY HTTP response**


.. code::

   HTTP/1.1 201 Created
   Content-Length: 0
   X-Copied-From-Last-Modified: Thu, 16 Jan 2014 21:19:45 GMT
   X-Copied-From: MySourceObject
   Last-Modified: Fri, 17 Jan 2014 18:22:57 GMT
   Etag: 451e372e48e0f6b1114fa0724aa79fa1
   Content-Type: text/html; charset=UTF-8
   X-Object-Meta-Test: testCF
   X-Trans-Id: txdcb481ad49d24e9a81107-0052d97501
   Date: Fri, 17 Jan 2014 18:22:57 GMT





**Example: Copy object using PUT HTTP response**


.. code::

   HTTP/1.1 201 Created
   Content-Length: 0
   X-Copied-From-Last-Modified: Thu, 16 Jan 2014 21:19:45 GMT
   X-Copied-From: MySourceObject
   Last-Modified: Fri, 17 Jan 2014 18:22:57 GMT
   Etag: 451e372e48e0f6b1114fa0724aa79fa1
   Content-Type: text/html; charset=UTF-8
   X-Object-Meta-Test: testCF
   X-Trans-Id: txdcb481ad49d24e9a81107-0052d97501
   Date: Fri, 17 Jan 2014 18:22:57 GMT




