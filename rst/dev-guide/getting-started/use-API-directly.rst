.. _gsg-use-API-directly:

Create and manage object storage
---------------------------------------------- 

You can use the simple examples in the following sections for basic Cloud Files  
requests that you will commonly use. Example requests are provided in
cURL, followed by the response.

Before running the examples, review the :ref:`Cloud Files concepts<concepts>`.

..  note:: 
    Generally, each time ``curl`` is invoked to perform an operation, a
    separate TCP/IP and SSL connection is created and then discarded. The
    language APIs, in contrast, are designed to reuse connections between
    operations and therefore provide much better performance. We recommend
    that you use one of the language APIs in your production applications
    and limit cURL to testing and troubleshooting.

For more information about all Cloud Files operations, see the
:ref:`API reference <api-reference>`.

.. include:: ../getting-started/create-storage-container.rst
.. include:: ../getting-started/upload-storage-object.rst
.. include:: ../getting-started/update-object-metadata.rst
.. include:: ../getting-started/retrieve-object.rst
.. include:: ../getting-started/delete-object.rst
.. include:: ../getting-started/delete-container.rst
.. include:: ../getting-started/show-account-details.rst
.. include:: ../getting-started/determine-storage-usage.rst
.. include:: ../getting-started/CDN-enabling-container.rst
.. include:: ../getting-started/view-CDN-container-details.rst
.. include:: ../getting-started/purge-CDN-data.rst
.. include:: ../getting-started/disable-CDN.rst
