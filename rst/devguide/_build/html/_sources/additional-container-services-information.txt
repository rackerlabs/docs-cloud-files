.. _cf-dg-container-services:

=========================================
Additional container services information
=========================================

This section provides additional metadata options for containers in
Cloud Files.

.. _cf-dg-container-acls:

==============================
Container access control lists
==============================

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
   everything in their Cloud Files account. However, the users specified in the 
   headers need to have a valid authentication token for the account to be able 
   to read objects in the container or write to the container.

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
see the blog post, `Create Cloud Files Container-Level Access Control
Policies. <http://www.rackspace.com/blog/create-cloud-files-container-level-access-control-policies/>`__

.. _cf-dg-container-quotas:

================
Container quotas
================

Users (most likely account administrators) who have the ability to set
container metadata can implement simple quotas on Cloud Files
containers. Setting container quotas can be useful for limiting
containers for non-admin users, FormPost uploads, or just as a sanity
check. (For information about FormPost, see :ref:`FormPost<cf-dg-formpost>`.)

Any object **PUT** operations that exceed a quota return a 413 response
(request entity too large) with a descriptive body.

Because the storage system is a true distributed system and because it
accepts simultaneous requests, the quotas might not be enforced exactly.
For example, if the quota is 5 GB and two users try to store a 5 GB file
at exactly the same time, both operations would be allowed to store the
file because at the time of both requests the container had sufficient
remaining quota.

Also, for chunked file uploads, the storage system cannot reject
transfers that will eventually exceed the quota because the storage
system does not know whether the end of the file will exceed the quota. (For 
more information about chunked file uploads, see :ref:`Chunked transfer encoding<cf-dg-chunked-transfer-encoding>`.)

You set quotas by adding metadata to the container. The available
metadata values are described in the following table.

**Table: Metadata values for setting container quotas**

+--------------------------------------+--------------------------------------+
| Metadata header                      | Description                          |
+======================================+======================================+
| ``X-Container-Meta-Quota-Bytes``     | Maximum size of the container, in    |
|                                      | bytes                                |
+--------------------------------------+--------------------------------------+
| ``X-Container-Meta-Quota-Count``     | Maximum number of objects in the     |
|                                      | container                            |
+--------------------------------------+--------------------------------------+

.. _cf-dg-access-log-delivery:

==========
Access log 
==========

You can use access log delivery to analyze the number of requests for
each object, the client IP address, and time-based usage patterns (such
as monthly or seasonal usage).

Access log delivery is set on the container, and every object in the
container is tracked. To enable access logs for a container, set the
metadata ``X-Container-Meta-Access-Log-Delivery`` header to ``True``. If
you have multiple containers that you want to track, you must set the
metadata header to ``TRUE`` for each container. When your first log is
delivered, the container .ACCESS\_LOGS is created. This container holds
the access logs for every container for which you turn on logging. Log
files exist until you delete them. To turn off logging, set the
``X-Container-Meta-Access-Log-Delivery`` header to ``FALSE``.

Log files are named according to the following pattern: container name,
log date, log hour, and MD5 hash. For example::

      Media/2012/10/01/16/096e6c4473f235db081deb51f42a8d98.log.gz

In this example, ``Media`` is the name of the container, 2012/10/01 is
the date (October 1, 2012), and 16 is the hour that the log file was
created. There might be multiple files for a given hour because the
storage system splits log files based on both time and log file size.
All times in the access logs are UTC time.

Within the gzip logs, the format of the entries is similar to National
Center for Supercomputing Applications (NCSA) combined log format, but
without cookies. The pattern follows. The dashes (*``-``*) denote fields
that the NCSA combined log format dictates be present but that Cloud
Files does not capture.

``client_ip - - [day/month/year:hour:minute:second timezone] “method request HTTP_version” return_code bytes_sent “referrer” “user_agent”``

The following example shows log entries.

**Example: Access log entries**

.. code::

       50.56.228.64 - - [27/08/2012:16:50:22 +0000] "PUT /v1/
            MossoCloudFS_bb88c7b9-ea5b-49af-82fc-376ff241963c/CharacterTest_%2521 
            HTTP/1.0" 401 0 "-" "python-requests/0.13.8 
            CPython/2.7.3 Linux/3.2.0-29-generic"
       50.56.228.64 - - [27/08/2012:16:53:49 +0000] "PUT /v1/
            MossoCloudFS_bb88c7b9-ea5b-49af-82fc-376ff241963c/CharacterTest_%2521
            /object_%2521 HTTP/1.0" 201 118 "-" "python-requests/0.13.8 
            CPython/2.7.3 Linux/3.2.0-29-generic"  
       50.56.228.64 - - [27/08/2012:16:53:47 +0000] "PUT /v1/
            MossoCloudFS_bb88c7b9-ea5b-49af-82fc-376ff241963c/CharacterTest_%2521 
            HTTP/1.0" 202 58 "-" "python-requests/0.13.8 
            CPython/2.7.3 Linux/3.2.0-29-generic"       
       50.56.228.64 - - [27/08/2012:16:50:36 +0000] "PUT /v1/
            MossoCloudFS_bb88c7b9-ea5b-49af-82fc-376ff241963c/CharacterTest_%2521 
            HTTP/1.0" 401 0 "-" "python-requests/0.13.8 
            CPython/2.7.3 Linux/3.2.0-29-generic"


