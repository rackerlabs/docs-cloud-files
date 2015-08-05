
.. THIS OUTPUT IS GENERATED FROM THE WADL. DO NOT EDIT.

Create or update object metadata
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    POST /v1/{account}/{container}/{object}

Sets or updates your object metadata. Metadata must be in the format ``X-Object-Meta-name`` where ``name`` is the name of your metadata. You can also assign ``X-Delete-At`` or ``X-Delete-After`` to expiring objects.

You can set or update your custom metadata for existing objects by sending a ``POST`` request to the object name. 

Metadata is set by using the header ``X-Object-Meta-name: value``, where ``name`` is the custom name for your metadata and ``value`` is the value.

You can also set values for ``X-Delete-At`` and ``X-Delete-After`` to set expirations for objects. 

For information about working with metadata when copying objects, see `Copy object <http://docs.rackspace.com/files/api/v1/cf-devguide/content/COPY_copyobject_v1__account___container___object__objectServicesOperations_d1e000.html>`__.

Deleting object metadataFor objects, the ``POST`` request to set metadata deletes all metadata that is not explicitly set in the request. In other words, ALL the object metadata is set at the time of the ``POST`` request. If you want to edit or remove one header, include all other headers in the ``POST`` request and leave out the header that you want to remove. This means that if you delete one entry without posting the others, the others will also be deleted at that time.

For example, you use a ``HEAD`` request to list object metadata and get the following results:

X-Object-Meta-Price: 50                    X-Object-Meta-Extra: DataThen you perform a ``POST`` request similar to the following example to set metadata on the same object that you listed above:

POST /v1/account/containName/objectName HTTP/1.1Host: storage.clouddrive.comX-Auth-Token: yourAuthTokenX-Object-Meta-Price: 45X-Object-Meta-Cost: 30Listing the object metadata again after the ``POST`` then shows the following results and ``X-Object-Meta-Extra`` no longer exists:

X-Object-Meta-Price: 45                    X-Object-Meta-Cost: 30To remove all metadata for an object, simply perform a ``POST`` request for the object with no metadata specified. 

Note that removing container metadata works differently. For more information, see `Delete container metadata <http://docs.rackspace.com/files/api/v1/cf-devguide/content/POST_deletecontainermeta_v1__account___container__containerServicesOperations_d1e000.html>`__.

A status code of 202 (Accepted) indicates success. Status code 404 (Not Found) is returned if the requested object does not exist. 

This operation does not require a request body and does return a response body.



This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|202                       |Accepted                 |The request was accepted |
|                          |                         |for processing.The       |
|                          |                         |length of the object     |
|                          |                         |content in the response  |
|                          |                         |body, in bytes. The MIME |
|                          |                         |type of the object.A     |
|                          |                         |unique transaction       |
|                          |                         |identifier for this      |
|                          |                         |request. The transaction |
|                          |                         |date and time.           |
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





This operation does not accept a request body.




**Example Update object metadata: HTTP request**


.. code::

    POST /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer/MyObject HTTP/1.1
    Host: storage.clouddrive.com
    X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c
    X-Object-Meta-Fruit: Apple
    X-Object-Meta-Veggie: Carrot


Response
""""""""""""""""





**Example Update object metadata: HTTP response**


.. code::

    HTTP/1.1 202 Accepted
    Date: Thu, 07 Jun 2007 20:59:39 GMT
    Content-Length: 0
    Content-Type: text/plain; charset=UTF-8
    X-Trans-Id: tx5ec7ab81cdb34ced887c8-0052d84ca4


