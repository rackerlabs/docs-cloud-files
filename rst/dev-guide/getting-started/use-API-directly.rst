.. _gsg-use-API-directly:

Create and manage object storage
---------------------------------------------- 

You can use the simple examples in the following sections for basic Cloud Files  
requests that you will commonly use. Example requests are provided in
cURL, followed by the response.

..  note:: 
    Generally, each time ``curl`` is invoked to perform an operation, a
    separate TCP/IP and SSL connection is created and then discarded. The
    language APIs, in contrast, are designed to reuse connections between
    operations and therefore provide much better performance. We recommend
    that you use one of the language APIs in your production applications
    and limit cURL to testing and troubleshooting.

Before running the examples, review the :ref:`Cloud Files concepts<concepts>`.

.. note:: 
     These examples use the ``$API_ENDPOINT``, ``$AUTH_TOKEN``, and ``$TENANT_ID`` environment 
     variables to specify the API endpoint, authentication token, and account ID values 
     for accessing the service. Make sure you 
     :ref:`configure these variables<configure-environment-variables>` before running the 
     code samples. 

For more information about all Cloud Files operations, see the
:ref:`API reference <api-reference>`.

.. include:: examples/create-storage-container.rst
.. include:: examples/upload-storage-object.rst
.. include:: examples/update-object-metadata.rst
.. include:: examples/retrieve-object.rst
.. include:: examples/delete-object.rst
.. include:: examples/delete-container.rst
.. include:: examples/show-account-details.rst
.. include:: examples/determine-storage-usage.rst
.. include:: examples/CDN-enabling-container.rst
.. include:: examples/view-CDN-container-details.rst
.. include:: examples/purge-CDN-data.rst
.. include:: examples/disable-CDN.rst
