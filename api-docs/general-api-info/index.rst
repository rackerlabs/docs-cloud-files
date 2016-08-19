.. _general-api-info:

=======================
General API information
=======================

The information in this section is relevant to all operations of the API.
For details about specific operations, see the
:ref:`Storage API reference <storage-api-reference>` and the :ref:`CDN API reference <cdn-api-reference>`.

The |apiservice| is implemented using a RESTful web
service interface. Like other Rackspace Cloud services, this service
shares a common token-based authentication system that allows seamless
access between products and services.

..  note::
    All requests to authenticate against and operate the service are performed
    using SSL over HTTP (HTTPS) on TCP port 443. For authentication instructions, see
    :ref:`Authenticate to the Rackspace Cloud <authenticate-to-cloud>`.

.. toctree:: :hidden:
   :maxdepth: 2

   operations-overview
   service-access
   service-version
   request-response
   limits
   response-codes
   role-based-access-control
   pseudo-hierarchical-folders-and-directories
