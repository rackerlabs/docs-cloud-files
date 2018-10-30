.. _service-access:

========================
Service access endpoints
========================

Cloud Files is a regionalized service. You can create your Cloud Files
containers in any Rackspace data center. The user of the service is
therefore responsible for appropriate replication, caching, and overall
maintenance of Cloud Files data across regional boundaries to other
Cloud Files servers.

.. tip::
   To help you decide which regionalized endpoint to use, read about
   :how-to:`special considerations for choosing a region <about-regions>`.


The endpoints to use for the storage service component of your Cloud
Files API calls are summarized in the following table. The first
endpoint listed for each region is externally accessible. The second
endpoint is accessed only from the internal ServiceNet.

**Table: Regionalized service endpoints for storage services**

+--------------------------+-------------------------------------------------------------------------------------------------------+
| Region                   |                                                                                                       |
+--------------------------+-------------------------------------------------------------------------------------------------------+
| Chicago (ORD)            | ``https://storage101.ord1.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee/``      |
+                          +-------------------------------------------------------------------------------------------------------+
|                          | ``https://snet-storage101.ord1.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee/`` |
+--------------------------+-------------------------------------------------------------------------------------------------------+
| Dallas/Ft. Worth (DFW)   | ``https://storage101.dfw1.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee/``      |
+                          +-------------------------------------------------------------------------------------------------------+
|                          | ``https://snet-storage101.dfw1.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee/`` |
+--------------------------+-------------------------------------------------------------------------------------------------------+
| Hong Kong (HKG)          | ``https://storage101.hkg1.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee/``      |
+                          +-------------------------------------------------------------------------------------------------------+
|                          | ``https://snet-storage101.hkg1.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee/`` |
+--------------------------+-------------------------------------------------------------------------------------------------------+
| London (LON)             | ``https://storage101.lon3.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee/``      |
+                          +-------------------------------------------------------------------------------------------------------+
|                          | ``https://snet-storage101.lon3.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee/`` |
+--------------------------+-------------------------------------------------------------------------------------------------------+
| Northern Virginia (IAD)  | ``https://storage101.iad3.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee/``      |
+                          +-------------------------------------------------------------------------------------------------------+
|                          | ``https://snet-storage101.iad3.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee/`` |
+--------------------------+-------------------------------------------------------------------------------------------------------+
| Sydney (SYD)             | ``https://storage101.syd2.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee/``      |
+                          +-------------------------------------------------------------------------------------------------------+
|                          | ``https://snet-storage101.syd2.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee/`` |
+--------------------------+-------------------------------------------------------------------------------------------------------+

**ServiceNet endpoints**

If you are working with cloud servers that are in one of the Rackspace
data centers, using the ServiceNet endpoint in the same data center has
no network costs and provides a faster connection. ServiceNet endpoints
are prefixed with ``snet-`` in the table “Regionalized service
endpoints for storage services”. ServiceNet is the data
center internet network. In the
:ref:`authentication service response<cloud-files-auth-response>`,
it is listed as ``internalURL``.

**Public endpoints**

If you are working with servers that are not in one of the Rackspace
data centers, you must use a public endpoint to connect. In the
:ref:`authentication service response<cloud-files-auth-response>`,
public endpoints are listed as ``publicURL``.
If you are working with servers in multiple data centers or have a mixed
environment where you have servers in your data centers and in Rackspace
data centers, use a public endpoint because it is accessible from all
the servers in the different environments.

Replace the sample MossoCloudFS information in the preceding table with
the actual MossoCloudFS information returned as part of the
:ref:`authentication service response<cloud-files-auth-response>`. This
information is
located after the final '/' in the ``publicURL`` field and the ``internalURL``
field in the ``cloudFiles`` section of the service catalog returned by the
authentication response.

.. tip:: If you do not know which data center you are working in or your
   account ID, you can find them in your Cloud Control Panel at
   :mycloud:`login.rackspace.com<>`.

.. note:: To avoid external bandwidth charges, your containers and servers must
   be in the same data center.

You might find it useful to locate your objects in more than one data
center to keep track of your data and backups. Specifically, if you
serve an audience in a particular region, you might find it helpful to
locate your Cloud Files objects as close to that region as possible.

The endpoints to use for the CDN management service component of your
Cloud Files API calls are summarized in the following table.

.. note:: If your audience is worldwide, consider using the Akamai content
   delivery network (CDN). The CDN speeds your content delivery because it
   is cached at edge locations around the globe, rather than being served
   from a single origin server.

**Table: Regionalized service endpoints for CDN management services**

+-------------------------+---------------------------------------------------------------------------------------+
| Region                  | Endpoint                                                                              |
+-------------------------+---------------------------------------------------------------------------------------+
| Chicago (ORD)           | ``https://cdn2.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee/`` |
+-------------------------+---------------------------------------------------------------------------------------+
| Dallas/Ft. Worth (DFW)  | ``https://cdn1.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee/`` |
+-------------------------+---------------------------------------------------------------------------------------+
| Hong Kong (HKG)         | ``https://cdn6.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee/`` |
+-------------------------+---------------------------------------------------------------------------------------+
| London (LON)            | ``https://cdn3.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee/`` |
+-------------------------+---------------------------------------------------------------------------------------+
| Northern Virginia (IAD) | ``https://cdn5.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee/`` |
+-------------------------+---------------------------------------------------------------------------------------+
| Sydney (SYD)            | ``https://cdn4.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee/`` |
+-------------------------+---------------------------------------------------------------------------------------+

As with the storage component service, replace the sample MossoCloudFS
information with the actual MossoCloudFS information returned as part of
the :ref:`authentication service response<cloud-files-auth-response>`.
For the CDN
management service, this information is located after the final '/' in the
``publicURL`` field in the ``cloudFilesCDN`` section of the service catalog
returned.
