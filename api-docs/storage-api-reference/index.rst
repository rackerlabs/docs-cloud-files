.. _storage-api-reference:

=====================
Storage API reference
=====================

This section describes each of the API operations provided by the Cloud Files
service for **storage services**.

Learn about the available |apiservice| resources and operations for storage,
and see request and response examples. You can use the |apiservice| operations
to interact directly with the service.

All requests are directed to the endpoints described in the ``cloudFiles``
section of the service catalog obtained during successful authentication. (For
more information, see
:ref:`Authenticate to the Rackspace Cloud<authenticate-to-cloud>` and
:ref:`Service access endpoints<service-access>`.)

Following are some requirements for the storage services component:

- Object and container names must be URL-encoded and UTF-8 encoded.

- Container names cannot exceed 256 bytes and cannot contain a forward slash
  (/).

- Object names cannot exceed 1024 bytes, but they have no character
  restrictions.

.. note::

     You can also perform operations by using the
     `Cloud Control Panel <https://login.rackspace.com/>`_.

.. toctree::
   :maxdepth: 2

   account-services-operations
   container-services-operations
   object-services-operations
