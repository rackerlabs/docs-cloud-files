.. _gsg-purge-cdn-data:

Purging an object from a CDN-enabled container 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To remove a CDN-enabled object from public access before the TTL
expires, you send an HTTP **DELETE** request with a valid authentication
token against the object to the CDN management service (or you can
create a support ticket to purge the entire container). Currently, you
can perform only 25 purges per account per day.

..  note:: 
    Remember that you must upload the objects to the container by using one
    of the storage service access endpoints. The CDN management service
    references the objects there.

Optionally, you can include a header with an email address to notify
that the object was purged.

An HTTP status code of 204 (No Content) in the response indicates that
the object was successfully queued to be purged.

Because there are so many edge servers around the world, purging an
object might take a long time. Be patient while waiting for the emailed
response.

 
**Example: cURL purge an object from a CDN-enabled container**

.. code::  

   curl -i -X DELETE https://cdn1.clouddrive.com/v1/yourAccountID/yourContainerName/yourObjectName /
   -H "X-Auth-Token: yourAuthToken" /
   -H "X-Purge-Email: yourEmail@yourDomain.com"      

.. code::  

   HTTP/1.1 204 No Content
   Content-Length: 0
   Content-Type: text/html; charset=UTF-8
   X-Trans-Id: tx45187f74dc814ddeb43af-005356c6e1hkg1
   Date: Tue, 22 Apr 2014 19:45:39 GMT   
