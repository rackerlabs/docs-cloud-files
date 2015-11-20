.. _gsg-show-account-details:

Showing account details
~~~~~~~~~~~~~~~~~~~~~~~

To show account details and list containers, you send an HTTP **GET**
request with a valid authentication token. Using the ``format`` query
parameter on the request causes the list to include details (``count``,
``bytes``, and ``name``) about each container. Without it, you receive
just a list of the container names.

An HTTP status code of 200 (OK) in the response indicates that the
account and container details were successfully retrieved.

 
**Example: cURL show account details**

.. code::  

   curl -i -X GET https://storage101.dfw1.clouddrive.com/v1/yourAccountID?format=json \
   -H "X-Auth-Token: yourAuthToken"  

.. code::  

   HTTP/1.1 200 OK
   Content-Length: 111
   X-Account-Object-Count: 573
   X-Timestamp: 1369081921.78518
   X-Account-Meta-Temp-Url-Key: ed6a04a9f70458575112811a9af5284e
   X-Account-Meta-Subject: Whaling
   X-Account-Bytes-Used: 14268918
   X-Account-Container-Count: 2
   Content-Type: application/json; charset=utf-8
   Accept-Ranges: bytes
   X-Trans-Id: tx6c802728f41b4804812ee-005356a3c8dfw1
   Date: Tue, 22 Apr 2014 17:15:52 GMT

     [
      {
        "count": 0,
        "bytes": 0,
        "name": "newcontainer"
      },
      {
        "count": 573,
        "bytes": 14268918,
        "name": "wordpressfiles"
      }
    ] 
