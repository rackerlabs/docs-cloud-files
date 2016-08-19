.. _cdn-api-reference:

=================
CDN API reference
=================

A CDN-enabled container is a public container that is served by the Akamai
content delivery network. The files in a CDN-enabled container are publicly
accessible and do not require an authentication token for read access. However,
uploading content into a CDN-enabled container is a secure operation and does
require a valid authentication token. (Private containers are not CDN-enabled
and the files in a private container are not publicly accessible.)

Learn about the available |apiservice| resources and operations for the content
delivery network (CDN), and see request and response examples. You can use the
|apiservice| operations to interact directly with the service.

This section provides further description for several of the API operations
described in the :ref:`Storage API reference <storage-api-reference>`. These
API operations have a specific purpose for the CDN service that is available in
Cloud Files.

You direct the REST API methods described in this section to the endpoints
listed in the ``cloudFilesCDN`` section of the service catalog that you obtain
during successful authentication. (For more information, see
:ref:`Authenticate to the Rackspace Cloud <authenticate-to-cloud>` section and
the :ref:`Service access endpoints <service-access>` section.)

.. note::

     You can also perform operations by using the
     :rax-devdocs:`Rackspace Command Line Interface (rack CLI) <#sdks>`, one
     of the language-specific :rax-devdocs:`software development kits <#sdks>`,
     or the `Cloud Control Panel <https://mycloud.rackspace.com/>`_.

.. toctree::
   :maxdepth: 2

   cdn-account-services-operations
   cdn-container-services-operations
   cdn-object-services-operations
   additional-cdn-service-information
