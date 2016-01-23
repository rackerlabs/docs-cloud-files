.. _expiring-objects:

Expiring objects
~~~~~~~~~~~~~~~~

When you perform a **PUT** or **POST** operation on an object and assign
it either an ``X-Delete-After`` or ``X-Delete-At`` header, the object is
scheduled for deletion. This feature is helpful for objects that you do
not want to permanently store, such as log files, recurring full backups
of a dataset, or documents or images that you know will be outdated at a
future time.

Objects that are assigned the ``X-Delete-At`` or ``X-Delete-After``
header are deleted within one day of the expiration time, and the object
stops being served immediately after the expiration time.

The ``X-Delete-At`` header requires a UNIX epoch timestamp, in integer
form. For example, 1348691905 represents Wed, 26 Sep 2012 20:38:25 GMT.
By setting the header to a specific epoch time, you indicate when you
want the object to expire, not be served, and be deleted completely from
the storage system.

The ``X-Delete-After`` header takes an integer number of seconds that
represents the amount of time from now when you want the object to be
deleted. The proxy server that receives the request converts this header
into an ``X-Delete-At`` header and calculates the deletion time using
its current time plus the value given in seconds.

To assign expiration headers to existing objects, use the **POST**
operation.

In the following example, the ``X-Delete-At`` header is assigned with a
UNIX epoch timestamp in integer form for Mon, 11 Jun 2012 15:38:25 GMT.
For example timestamps and a batch converter, go to
http://www.epochconverter.com/.

**Example: X-Delete-At: HTTP request**

.. code::

    PUT /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer/MyObject HTTP/1.1
    Host: storage.clouddrive.com
    X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c
    Content-Type: image/jpeg
    X-Delete-At: 1339429105

In the following example, the ``X-Delete-After`` header is assigned a
value in seconds, equivalent to 10 days. After this time, the object
expires.

**Example: X-Delete-After: HTTP request**

.. code::

    PUT /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer/MyObject HTTP/1.1
    Host: storage.clouddrive.com
    X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c
    Content-Type: image/jpeg
    X-Delete-After: 864000
