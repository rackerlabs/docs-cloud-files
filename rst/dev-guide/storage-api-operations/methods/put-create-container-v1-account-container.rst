
.. THIS OUTPUT IS GENERATED FROM THE WADL. DO NOT EDIT.

.. _create-container:

Create container
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    PUT /v1/{account}/{container}

This operation creates a Cloud Files container. Containers are storage compartments for your data. The URL-encoded name must be no more than 256 bytes and cannot contain a forward slash character (/). You can create up to 500,000 containers in your Cloud Files account.

You can assign custom metadata for containers by including additional HTTP headers with an ``X-Container-Meta-`` prefix on the ``POST`` request. For details on setting custom metadata, see :ref:`Create or update account metadata <create-or-update-account-metadata>`. 

Using custom container metadata, you can create information in the header to effectively tag a container. The container metadata restrictions are the same as the restrictions for object metadata. You can have a maximum of 4096 bytes of metadata for the container, with a maximum of 90 distinct metadata items. Each distinct metadata item can have a name length of up to 128 characters with a maximum of 256 bytes in the value. Any valid UTF-8 encoded string value is allowed for metadata. In addition for custom metadata, we recommend that you URL-encode any non-ASCII values by using a % symbol followed by the two-digit hexadecimal ISO-Latin code for the character.

A status code of 201 (Created) indicates that the container was created as requested. Container ``PUT`` requests are idempotent, and a code of 202 (Accepted) is returned if the container existed prior to the request. If you make a ``PUT`` request to a container with an ``X-Container-Meta-`` prefix in the header, your ``GET`` or ``HEAD`` request responses carry the metadata prefix from the container in subsequent requests.

This operation does not require a request body and does not return a response body.



This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|201 202                   |Created or Accepted      |The request has been     |
|                          |                         |fulfilled. For 201       |
|                          |                         |Created, the new         |
|                          |                         |container has been       |
|                          |                         |created. For 202         |
|                          |                         |Accepted, the request    |
|                          |                         |has been accepted for    |
|                          |                         |processing.              |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad Request              |The request could not be |
|                          |                         |understood by the server |
|                          |                         |due to malformed syntax. |
+--------------------------+-------------------------+-------------------------+


Request
""""""""""""""""


This table shows the header parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|X-Auth-Token              |String *(Required)*      |Authentication token.    |
+--------------------------+-------------------------+-------------------------+
|X-Container-Meta-name     |String *(Optional)*      |Custom container         |
|                          |                         |metadata. Replace        |
|                          |                         |``name`` at the end of   |
|                          |                         |the header with the name |
|                          |                         |for your metadata.       |
+--------------------------+-------------------------+-------------------------+
|X-Container-Read          |String *(Optional)*      |Sets an access control   |
|                          |                         |list (ACL) that grants   |
|                          |                         |read access. This header |
|                          |                         |can contain a comma-     |
|                          |                         |delimited list of users  |
|                          |                         |that can read the        |
|                          |                         |container (allows the    |
|                          |                         |GET method for all       |
|                          |                         |objects in the           |
|                          |                         |container).              |
+--------------------------+-------------------------+-------------------------+
|X-Container-Write         |String *(Optional)*      |Sets an ACL that grants  |
|                          |                         |write access. This       |
|                          |                         |header can contain a     |
|                          |                         |comma-delimited list of  |
|                          |                         |users that can write to  |
|                          |                         |the container (allows    |
|                          |                         |PUT, POST, COPY, and     |
|                          |                         |DELETE methods for all   |
|                          |                         |objects in the           |
|                          |                         |container).              |
+--------------------------+-------------------------+-------------------------+
|X-Versions-Location       |String *(Optional)*      |Enables versioning on    |
|                          |                         |this container. The      |
|                          |                         |value is the name of     |
|                          |                         |another container. You   |
|                          |                         |must UTF-8-encode and    |
|                          |                         |then URL-encode the name |
|                          |                         |before you include it in |
|                          |                         |the header. To disable   |
|                          |                         |versioning, set the      |
|                          |                         |header to an empty       |
|                          |                         |string.                  |
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




**Example Create container: HTTP request**


.. code::

   PUT /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer HTTP/1.1
   Host: storage.clouddrive.com
   X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c
   





**Example Create container with metadata: HTTP request**


.. code::

   PUT /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer HTTP/1.1
   Host: storage.clouddrive.com
   X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c
   X-Container-Meta-InspectedBy: JackWolf





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




This operation does not return a response body.





**Example Create container: HTTP response**


.. code::

   HTTP/1.1 201 Created
   Content-Length: 0
   Content-Type: text/html; charset=UTF-8
   X-Trans-Id: tx7f6b7fa09bc2443a94df0-0052d58b56
   Date: Tue, 14 Jan 2014 19:09:10 GMT





**Example Create container with metadata: HTTP response**


.. code::

   HTTP/1.1 201 Created
   Content-Length: 0
   Content-Type: text/html; charset=UTF-8
   X-Trans-Id: tx06021f10fc8642b2901e7-0052d58f37
   Date: Tue, 14 Jan 2014 19:25:43 GMT




