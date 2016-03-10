
.. _delete-cdn-enabled-object:

Delete CDN-enabled object
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    DELETE /v1/{account}/{container}/{object}

This operation deletes CDN-enabled objects.

When you find it necessary to remove a CDN-enabled object from public access before the TTL expires, you can perform a ``DELETE`` operation against the object, or you can create a support ticket to purge the entire container.

.. warning::
   You request this operation against a CDN management services URI, such as ``https://cdn2.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee``/, as shown in the table “Regionalized service endpoints for CDN management service” in the :ref:`Service Access endpoints <service-access>` section. If you use a Storage management services URI by mistake, you delete your object.
   
   

.. note::
   You should limit object purges to situations in which serious personal, business, or security consequences could occur if the object remained publicly accessible on the CDN (for example, when someone publishes your company's quarterly earnings too early).
   
   

You can purge objects from the CDN in the following ways: 

**By using DELETE in the API**

You can manually purge CDN-enabled objects without having to wait for the TTL to expire, and you can optionally be notified by email that the object has been purged.

You can use the ``DELETE`` operation against a maximum of 25 objects per day using the API.

An attempt to delete more objects results in a 498 (Rate Limited) status code.

Here is an example response for hitting the purge rate limit:

.. code::

   $ curl -i -XDELETE -H'x-auth-token: f064c46a782c444cb4ba4b6434288f7c' https://cdn1.clouddrive.com/v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainter/MyObject 
   HTTP/1.1 498 Rate Limited 
   Content-Length: 42 
   Content-Type: text/html; charset=UTF-8 
   X-Trans-Id: txb63f31d26bf84c058542b-0055101cd0dfw1 
   Date: Mon, 23 Mar 2015 14:01:52 GMT

**By creating a support ticket to purge an entire container**

The 25-object limit does not apply when purging an entire container through Support.




.. note::
   To prevent the container from going back to the CDN, first change the ``X-CDN-Enabled`` flag to ``False`` as shown in :ref:`CDN-enable and CDN-disable a container <put-cdn-enable-and-cdn-disable-a-container>`.   
   

The system purges the object from the CDN and sends an email to the indicated address or addresses. If you want to notify more than one person about the deletion, you can enter a comma-separated list of addresses. The email address is optional.

A status code of 204 (No Content) indicates success. Status code 498 (Rate Limited) indicates that the account has reached its 25 object daily purge limit for CDN-enabled objects. Status code 403 (Forbidden) indicates that an authorization problem occurred.

Because there are so many edge servers around the world, purging objects might take a long time. Be patient while waiting for a response.

This operation does not return a response body.



This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|204                       |No Content               |The server fulfilled the |
|                          |                         |request but does not     |
|                          |                         |need to return a body.   |
+--------------------------+-------------------------+-------------------------+
|403                       |Forbidden                |The server refused to    |
|                          |                         |respond to request.      |
+--------------------------+-------------------------+-------------------------+
|498                       |Rate Limited             |The account has reached  |
|                          |                         |the 25 object daily      |
|                          |                         |purge limit for CDN-     |
|                          |                         |enabled objects.         |
+--------------------------+-------------------------+-------------------------+


Request
""""""""""""""""




This table shows the URI parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|{account}                 |String *(Required)*      |Your unique account      |
|                          |                         |identifier.              |
+--------------------------+-------------------------+-------------------------+
|{container}               |String *(Required)*      |The unique identifier of |
|                          |                         |the container.           |
+--------------------------+-------------------------+-------------------------+
|{object}                  |String *(Required)*      |The unique identifier of |
|                          |                         |the object.              |
+--------------------------+-------------------------+-------------------------+





This operation does not accept a request body.




**Example: Delete CDN-enabled object HTTP request**


.. code::

   DELETE /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer/MyObject HTTP/1.1
   Host: cdn2.clouddrive.com
   X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c
   X-Purge-Email: user@domain.com, user2@domain.com





Response
""""""""""""""""




This operation does not return a response body.






**Example: Delete CDN-enabled object HTTP response**


.. code::

   HTTP/1.1 204 No Content
   Content-Type: text/html; charset=UTF-8
   Content-Length: 0
   X-Trans-Id: txd57d75dcd51e4a79a886d-0055101ecford1
   Date: Mon, 23 Mar 2015 14:10:25 GMT




