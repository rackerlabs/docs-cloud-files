.. _api-operations-for-cdn-services:

====================================
API operations for CDN services
====================================

This section provides further description for several of the API operations described in “API operations for storage services.” These API operations have a specific purpose for the content delivery network (CDN) service that is available in Cloud Files.

You direct the REST API methods described in this chapter to the endpoints listed in the cloudFilesCDN section of the service catalog that you obtain during successful authentication. (For more information, see :ref:`Authentication <auth>` section and the :ref:`Service access endpoints <service-access>` section.)

A CDN-enabled container is a public container that is served by the Akamai content delivery network. The files in a CDN-enabled container are publicly accessible and do not require an authentication token for read access. However, uploading content into a CDN-enabled container is a secure operation and does require a valid authentication token. (Private containers are not CDN-enabled and the files in a private container are not publicly accessible.)