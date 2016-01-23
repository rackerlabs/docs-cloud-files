.. _cdn-object-services-operations:

CDN object services operations
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can perform the operation described in this section on objects in your Cloud Files CDN-enabled containers.

The examples in this section use sample values for the following:

- account — for example, MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123

- X-Auth-Token — for example, f064c46a782c444cb4ba4b6434288f7c

- container — for example, MyContainer

- object — for example, MyObject

For your own requests, you must use your own account information, authentication token, container names, and object names. For more information, see :ref:`Authentication <auth>`. Your authentication token and your account information are in the service catalog that is produced.

.. warning::
   You request this operation against a CDN management services URI, such as ``https://cdn2.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee``/, as shown in  the table “Regionalized service endpoints for CDN management services” in the :ref:`Service access endpoints <service-access>` section. If you use a Storage management services URI by mistake, you delete your object.        

.. include:: methods/delete-delete-cdn-enabled-object-v1-account-container-object.rst
  
