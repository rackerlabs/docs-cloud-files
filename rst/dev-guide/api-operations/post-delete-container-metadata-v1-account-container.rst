
.. THIS OUTPUT IS GENERATED FROM THE WADL. DO NOT EDIT.

Delete container metadata
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    POST /v1/{account}/{container}

Deletes container metadata.

To delete a metadata header, use a ``POST`` operation. You send the ``POST`` operation to the container with the header ``X-Remove-Container-Meta-name: value``, where ``name`` is the name of the metadata you want to delete and ``value`` is any value and is not used. 

To set and edit your custom metadata, see `Create or update container metadata <http://docs.rackspace.com/files/api/v1/cf-devguide/content/POST_updateacontainermeta_v1__account___container__containerServicesOperations_d1e000.html>`__.

Note that updating and deleting object metadata works differently. For an example, see `Create or update object metadata <http://docs.rackspace.com/files/api/v1/cf-devguide/content/POST_updateaobjmeta_v1__account___container___object__objectServicesOperations_d1e000.html>`__.

A status code of 200 through 299 indicates success. If the container does not exist, a status code of 404 (Not Found) is returned.

This operation does not require a request body and does not return a response body.



This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|204                       |No Content               |The request succeeded.   |
|                          |                         |The server fulfilled the |
|                          |                         |request but does not     |
|                          |                         |need to return a body.   |
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
|X-Remove-Container-Meta-  |String *(Required)*      |The metadata to be       |
|name                      |                         |deleted. Replace         |
|                          |                         |``name`` at the end of   |
|                          |                         |the header with the name |
|                          |                         |for your metadata.       |
+--------------------------+-------------------------+-------------------------+
|X-Container-Read          |String *(Optional)*      |The access control list  |
|                          |                         |(ACL) that grants read   |
|                          |                         |access. If not set, this |
|                          |                         |header is not returned   |
|                          |                         |by this operation. This  |
|                          |                         |header can contain a     |
|                          |                         |comma-delimited list of  |
|                          |                         |users that can read the  |
|                          |                         |container (allows the    |
|                          |                         |GET method for all       |
|                          |                         |objects in the           |
|                          |                         |container).              |
+--------------------------+-------------------------+-------------------------+
|X-Container-Write         |String *(Optional)*      |The ACL that grants      |
|                          |                         |write access. If not     |
|                          |                         |set, this header is not  |
|                          |                         |returned by this         |
|                          |                         |operation. This header   |
|                          |                         |can contain a comma-     |
|                          |                         |delimited list of users  |
|                          |                         |that can write to the    |
|                          |                         |container (allows PUT,   |
|                          |                         |POST, COPY, and DELETE   |
|                          |                         |methods for all objects  |
|                          |                         |in the container).       |
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





This operation does not accept a request body.




**Example Delete container metadata: HTTP request**


.. code::

    POST /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer HTTP/1.1
    Host: storage.clouddrive.com
    X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c
    X-Remove-Container-Meta-Subject: x


Response
""""""""""""""""


This table shows the header parameters for the response:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|Content-Length            |String *(Required)*      |The length of the        |
|                          |                         |response body that       |
|                          |                         |contains the list of     |
|                          |                         |names. If the operation  |
|                          |                         |fails, this value is the |
|                          |                         |length of the error text |
|                          |                         |in the response body.    |
+--------------------------+-------------------------+-------------------------+
|Content-Type              |String *(Required)*      |The MIME type of the     |
|                          |                         |list of names. If the    |
|                          |                         |operation fails, this    |
|                          |                         |value is the MIME type   |
|                          |                         |of the error text in the |
|                          |                         |response body.           |
+--------------------------+-------------------------+-------------------------+
|X-Trans-Id                |Uuid *(Required)*        |A unique transaction     |
|                          |                         |identifier for this      |
|                          |                         |request.                 |
+--------------------------+-------------------------+-------------------------+
|Date                      |Datetime *(Required)*    |The transaction date and |
|                          |                         |time.                    |
+--------------------------+-------------------------+-------------------------+







**Example Delete container metadata: HTTP response**


.. code::

    HTTP/1.1 204 No Content
    Date: Thu, 09 Jan 2014 22:28:22 GMT
    Content-Length: 0
    Content-Type: text/html; charset=UTF-8
    X-Trans-Id: txe749a717ee5e4da7a6895-0052cf2286dfw1
    


