.. _cf-dg-chunked-transfer-encoding:

=========================
Chunked transfer encoding
=========================

You can upload data without knowing in advance the amount of data to be
uploaded. You can do this by specifying the HTTP header
``Transfer-Encoding: chunked`` and not using a ``Content-Length``
header. A good use of this feature would be performing a database dump,
piping the output to gzip, and then piping the gzip file directly to
Cloud Files without writing the data to disk to compute the file size.
If you attempt to upload more than 5 GB, the server closes the
connection and removes the previously sent data from the system. You
must ensure that the data that you transfer is less than 5 GB or split
it into 5 GB chunks, each in its own storage object.

If you have files that are larger than 5 GB and you want to use Cloud
Files, you can segment the files before you upload them, upload them to
the same container, and then use a manifest file to allow downloading of
a concatenated object that contains all the segmented objects. For more 
information, see :ref:`Creating large objects <cf-dg-large-objects>`.

**Example: Upload unspecified quantity of data: HTTP request**

.. code::

    PUT /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer/MyObject HTTP/1.1
    Host: storage.clouddrive.com
    X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c
    Transfer-Encoding: chunked
    X-Object-Meta-PIN: 1234

**Example: Upload unspecified quantity of data response**

.. code::

    19
    A bunch of data broken up
    D
    into chunks.
    0

