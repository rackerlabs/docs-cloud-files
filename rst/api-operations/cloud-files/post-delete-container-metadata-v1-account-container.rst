
.. THIS OUTPUT IS GENERATED FROM THE WADL. DO NOT EDIT.

=============================================================================
Delete Container Metadata -  Rackspace Cloud Files™ Developer Guide
=============================================================================

Delete Container Metadata
~~~~~~~~~~~~~~~~~~~~~~~~~

`Request <post-delete-container-metadata-v1-account-container.html#request>`__
`Response <post-delete-container-metadata-v1-account-container.html#response>`__

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
|                          |                         |need to return a         |
|                          |                         |body.The length of the   |
|                          |                         |response body that       |
|                          |                         |contains the list of     |
|                          |                         |names. If the operation  |
|                          |                         |fails, this value is the |
|                          |                         |length of the error text |
|                          |                         |in the response body.The |
|                          |                         |MIME type of the list of |
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
|404                       |Not Found                |The requested resource   |
|                          |                         |was not found.           |
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








**Example Delete container metadata: HTTP request**


.. code::

    POST /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer HTTP/1.1
    Host: storage.clouddrive.com
    X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c
    X-Remove-Container-Meta-Subject: x


Response
^^^^^^^^^^^^^^^^^^





**Example Delete container metadata: HTTP response**


.. code::

    HTTP/1.1 204 No Content
    Date: Thu, 09 Jan 2014 22:28:22 GMT
    Content-Length: 0
    Content-Type: text/html; charset=UTF-8
    X-Trans-Id: txe749a717ee5e4da7a6895-0052cf2286dfw1
    

