.. _object-services-operations:

Object services operations
~~~~~~~~~~~~~~~~~~~~~~~~~~

You can perform the operations in the following table on objects in your Cloud
Files containers.

The examples in this section use sample values for the following:

- account — for example, MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123

- X-Auth-Token — for example, f064c46a782c444cb4ba4b6434288f7c

- container — for example, MyContainer

- object — for example, MyObject

For your own requests, you must use your own account information,
authentication token, container names, and object names. For more information,
see the :ref:`Authentication <auth>` section. Your authentication token and
your account information are in the service catalog that is produced.

.. include:: methods/get-get-object-content-and-metadata-v1-account-container-object.rst
.. include:: methods/put-create-or-update-object-v1-account-container-object.rst
.. include:: methods/delete-delete-object-v1-account-container-object.rst
.. include:: methods/copy-copy-object-v1-account-container-object.rst
.. include:: methods/head-show-object-metadata-v1-account-container-object.rst
.. include:: methods/post-create-or-update-object-metadata-v1-account-container-object.rst
