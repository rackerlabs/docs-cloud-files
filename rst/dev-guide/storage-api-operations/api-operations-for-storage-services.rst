.. _api-operations-for-storage-services:

====================================
API operations for storage services
====================================

This section describes each of the API operations provided by the Cloud Files service for storage services.

All requests are directed to the endpoints described in the cloudFiles section of the service catalog obtained during successful authentication. (For more information, see “Authentication” section and the “Service access endpoints” section.)

Following are some requirements for the storage services component:

- Object and container names must be URL-encoded and UTF-8 encoded.

- Container names cannot exceed 256 bytes and cannot contain a forward slash (/).

- Object names cannot exceed 1024 bytes, but they have no character restrictions.