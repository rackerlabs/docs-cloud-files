=========================================
Additional container services information
=========================================

This section provides additional metadata options for containers in
Cloud Files.

Container access control lists
------------------------------

The Cloud Files access control list (ACL) feature allows account owners
to specify read or write access to a particular container for a
particular user.

Cloud Files ACLs provide the following metadata headers that you use to
define container-level access policies:

-  ``X-Container-Read`` – This header specifies a comma-delimited list
   of users that can read the container (allows the GET method for all
   objects in the container).

-  ``X-Container-Write`` – This header specifies a comma-delimited list
   of users that can write to the container (allows PUT, POST, COPY, and
   DELETE methods for all objects in the container).

Space before or after a comma in the comma-delimited list of users is
acceptable. Valid values for these headers are zero to many users.

You can set these headers only on containers, and they apply to all
objects within the container.

.. note:: The account owner does not need to be included as a user in the
   headers because the account owner always has read and write access to
   everything in their Cloud Files account.

However, the users specified in the headers need to have a valid
authentication token for the account to be able to read objects in the
container or write to the container.

You can use the operation to show container metadata to show the absence
of the ``X-Container-Read`` or ``X-Container-Write`` header for an
existing container, such as ``MyContainer`` in the following example.

**Example: Show container metadata before adding ACL headers: HTTP
request**

.. code::

    HEAD /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer HTTP/1.1
    Host: storage.clouddrive.com
    X-Storage-Token: 182f9c0af0e828cfe3281767d29d19f4 

**Example: Show container metadata before adding ACL headers: HTTP
response**

.. code::

    HTTP/1.1 204 No Content
    X-Container-Object-Count: 2 
    X-Container-Bytes-Used: 76 
    Accept-Ranges: bytes 
    X-Trans-Id: tx3aa52e951fc64b63bc1fda27902b9bd3 
    Content-Length: 80 
    Date: Mon, 07 Apr 2014 01:29:22 GMT 

Update the existing container to set the ``X-Container-Read`` and
``X-Container-Write`` metadata headers to enable read and write access
for ``user1``, ``user2``, and ``user3``.

**Example: Update container to add ACL headers: HTTP request**

.. code::

    POST /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer HTTP/1.1
    Host: storage.clouddrive.com
    X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c
    X-Container-Read: user1, user2, user3
    X-Container-Write: user1, user2, user3

Repeat the operation to show container metadata and confirm the metadata
change.

**Example: Show container metadata after adding ACL headers: HTTP
request**

.. code::

    HEAD /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer HTTP/1.1
    Host: storage.clouddrive.com
    X-Storage-Token: 182f9c0af0e828cfe3281767d29d19f4 

**Example: Show container metadata after adding ACL headers: HTTP
response**

.. code::

    HTTP/1.1 204 No Content
    X-Container-Object-Count: 2
    X-Container-Read: user1, user2, user3
    X-Container-Write: user1, user2, user3
    X-Container-Bytes-Used: 76
    Accept-Ranges: bytes
    X-Trans-Id: txb40eb86d949345f7bc66b01e8b63c3a5
    Content-Length: 80
    Date: Mon, 07 Apr 2014 02:20:12 GMT

For more information about ACLS and using them with RBAC,
see the blog post, `"Create Cloud Files Container-Level Access Control
Policies". <http://www.rackspace.com/blog/create-cloud-files-container-level-access-control-policies/>`__
