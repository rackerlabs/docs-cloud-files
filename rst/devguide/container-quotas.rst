================
Container quotas
================

Users (most likely account administrators) who have the ability to set
container metadata can implement simple quotas on Cloud Files
containers. Setting container quotas can be useful for limiting
containers for non-admin users, FormPost uploads, or just as a sanity
check.

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
system does not know whether the end of the file will exceed the quota.

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

