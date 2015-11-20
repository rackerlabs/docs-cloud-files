Using the API directly by using cURL 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This chapter contains simple examples for authentication and some basic
Cloud Files requests that you will commonly use. Example requests are
provided in cURL, followed by the response.

-  Generating an authentication token
-  Get your credentials 
-  Send the authentication request
-  Receive the token 
-  Creating a storage container 
-  Uploading an object 
-  Updating object metadata
-  Retrieving an object 
-  Deleting an object 
-  Deleting a container 
-  Showing account details 
-  Determining storage usage 
-  CDN-enabling the container and setting a TTL 
-  Viewing CDN-enabled container details 
-  Purging an object from a CDN-enabled container 
-  Disabling CDN for a container 

..  note:: 
    Generally, each time ``curl`` is invoked to perform an operation, a
    separate TCP/IP and SSL connection is created and then discarded. The
    language APIs, in contrast, are designed to reuse connections between
    operations and therefore provide much better performance. We recommend
    that you use one of the language APIs in your production applications
    and limit cURL to testing and troubleshooting.

For more information about all Cloud Files operations, see the :ref:`API reference <api-reference>`.
