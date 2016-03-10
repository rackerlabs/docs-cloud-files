.. _gsg-determine-storage-usage:

Determining storage usage
~~~~~~~~~~~~~~~~~~~~~~~~~

To determine how much data you have stored in the system and the number
of containers you are using, you send an HTTP **HEAD** request with a
valid authentication token.

An HTTP status code of 204 (No Content) in the response indicates that
the storage data was successfully retrieved. The HTTP headers in the
response indicate the number of containers in this storage account and
the total bytes stored for the entire account.

 
**Example: cURL determine storage usage request**

.. code::  

   curl -i -X HEAD $API_ENDPOINT/v1/$TENANT_ID \
   -H "X-Auth-Token: $AUTH_TOKEN" 

**Example: Determine storage usage response**

.. code::  

   HTTP/1.1 204 No Content
   Content-Length: 0
   X-Account-Object-Count: 573
   X-Timestamp: 1369081921.78518
   X-Account-Meta-Temp-Url-Key: ed6a04a9f70458575112811a9af5284e
   X-Account-Meta-Subject: Whaling
   X-Account-Bytes-Used: 14268918
   X-Account-Container-Count: 2
   Content-Type: text/plain; charset=utf-8
   Accept-Ranges: bytes
   X-Trans-Id: tx0618e82d44394a6b8c5fb-005356a46fdfw1
   Date: Tue, 22 Apr 2014 17:18:39 GMT
