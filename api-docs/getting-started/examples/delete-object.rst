.. _gsg-delete-object:

Deleting an object
~~~~~~~~~~~~~~~~~~~

To delete an object in a container, you send an HTTP **DELETE** request
with a valid authentication token.

An HTTP status code of 204 (No Content) in the response indicates that
the object was successfully deleted.

Both the object data and metadata are removed from the storage system.
Object deletion is processed immediately at the time of the request. Any
subsequent **GET**, **HEAD**, **POST**, **PUT**, or **DELETE**
operations return a 404 (Not Found) error (unless object versioning is
on and other versions exist). For more information about object
versioning, see the *Cloud Files Developer Guide*.

**Example: cURL delete an object request**

.. code::

   curl -i -X DELETE $API_ENDPOINT/v1/$TENANT_ID/yourContainerName/yourObjectName \
   -H "X-Auth-Token: $AUTH_TOKEN"

**Example: Delete an object response**

.. code::

   HTTP/1.1 204 No Content
   Content-Length: 0
   Content-Type: text/html; charset=UTF-8
   X-Trans-Id: tx32fae72bccc94cb68d605-005356a2badfw1
   Date: Tue, 22 Apr 2014 17:11:22 GMT
