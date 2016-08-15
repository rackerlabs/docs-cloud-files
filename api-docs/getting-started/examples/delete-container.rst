.. _gsg-delete-container:

Deleting a container
~~~~~~~~~~~~~~~~~~~~

To delete a container, you send an HTTP **DELETE** request with a valid
authentication token. The container must be empty before you can delete
it.

An HTTP status code of 204 (No Content) in the response indicates that
the container was successfully deleted.

**Example: cURL delete a container request**

.. code::

   curl -i -X DELETE $API_ENDPOINT/v1/$TENANT_ID/yourContainerName \
   -H "X-Auth-Token: $AUTH_TOKEN"

**Example: Delete a container response**

.. code::

   HTTP/1.1 204 No Content
   Content-Length: 0
   Content-Type: text/html; charset=UTF-8
   X-Trans-Id: tx4b8836bcc20a457d9bbe4-005356a30fdfw1
   Date: Tue, 22 Apr 2014 17:12:47 GMT
