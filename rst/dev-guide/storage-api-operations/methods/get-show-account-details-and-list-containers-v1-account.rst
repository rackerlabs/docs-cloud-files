
.. THIS OUTPUT IS GENERATED FROM THE WADL. DO NOT EDIT.

.. _getaccount-details-and-list-containers:

Show account details and list containers
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /v1/{account}

This operation lists the storage containers in your account and sorts them by name. You perform the operation against your storage account URL.

The list is limited to 10,000 containers at a time. For information on limiting and navigating the list, see the following section, "Controlling a Large List of Containers". 

Container names are sorted based on a binary comparison, a built-in collating function that compares string data by using SQLite's ``memcmp()`` function, regardless of text encoding. For more information, see `http://www.sqlite.org/datatype3.html#collation <http://www.sqlite.org/datatype3.html#collation>`__.

A list of containers is returned in the response body, one container per line. 

The character sequence used to create the newline that separates the container names is a single \n. If you want to parse these listings, you send an ``Accept: application/json`` or ``Accept: application/xml`` header with the request to get the results in JSON or XML.

An HTTP response status code of 200 through 299 indicates success. A 200 (OK) code is returned if there are containers, and a 204 (No Content) code is returned if there are no containers.

**Format Container List**

If you append the ``?format=xml`` or ``?format=json`` query parameter to the storage account URL, the service returns container information serialized in the specified format. To format your results, you must place this query parameter before any other parameters. 

The example responses in this section are formatted for readability. 

**Controlling a Large List of Containers**

A ``GET`` operation on the storage account URL returns a list of up to 10,000 container names. You can control and limit this list of results by using the ``marker``, ``end_marker``, and ``limit`` parameters. These parameters provide a mechanism for iterating through the entire list of containers. 

The ``marker`` parameter tells Cloud Files where to begin your list of containers, and the ``end_marker`` parameter specifies where to end the list. You can use them independently or together, separated by an ampersand ( ``&`` ). If you do not specify them, your list displays up to 10,000 containers. Note that the ``marker`` and ``end_marker`` values must be URL-encoded before you send the HTTP request.

You can use the ``limit`` parameter to reduce the number of returned objects. 

If the number of returned items equals the ``limit`` used (or 10,000 if no ``limit`` was specified), you can assume there are more object names.

.. note::
   At this time, a ``prefix`` query parameter is not supported at the account level.
   
   

As an example, start with an account that has five container names, as follows:

.. code::
 
   apples 
   bananas 
   kiwis 
   oranges 
   pears

Use a limit of 2 to show how things work:

.. code::

   GET /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123?limit=2 
   Host: storage.clouddrive.com 
   X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c 
   
   apples 
   bananas

Because the operation returned two items, assume there are more container names to list and make another request with a marker of the last item returned:

.. code::

   GET /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123?limit=2 & marker=bananas 
   Host: storage.clouddrive.com 
   X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c 
   
   kiwis 
   oranges 

Again, two items are returned, and you assume that there might be more. So you make another GET request for two more:

.. code::

   GET /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123?limit=2 & marker=oranges 
   Host: storage.clouddrive.com 
   X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c 
   
   pears 

This one-item response shows fewer than the limit of 2 container names requested, and indicates that this is the end of the list.

By using the ``end_marker`` parameter, you can limit the result set to container names less than the given value.

.. code::

   GET /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123?end_marker=oranges 
   Host: storage.clouddrive.com 
   X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c 
   
   apples 
   bananas 
   kiwis



This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |OK                       |The request succeeded.   |
+--------------------------+-------------------------+-------------------------+
|204                       |No Content               |The request succeeded.   |
|                          |                         |The server fulfilled the |
|                          |                         |request but does not     |
|                          |                         |need to return a body.   |
+--------------------------+-------------------------+-------------------------+
|404                       |Not Found                |The requested resource   |
|                          |                         |was not found.           |
+--------------------------+-------------------------+-------------------------+


Request
""""""""""""""""


This table shows the header parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|X-Auth-Token              |String *(Required)*      |Authentication token.    |
+--------------------------+-------------------------+-------------------------+
|Accept                    |String *(Optional)*      |Instead of using the     |
|                          |                         |``format`` query         |
|                          |                         |parameter, set this      |
|                          |                         |header to                |
|                          |                         |``application/json``,    |
|                          |                         |``application/xml``, or  |
|                          |                         |``text/xml``.            |
+--------------------------+-------------------------+-------------------------+




This table shows the URI parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|{account}                 |String                   |Your unique account      |
|                          |                         |identifier.              |
+--------------------------+-------------------------+-------------------------+



This table shows the query parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|limit                     |Int *(Optional)*         |For an integer value n,  |
|                          |                         |limits the number of     |
|                          |                         |results to n values.     |
+--------------------------+-------------------------+-------------------------+
|marker                    |String *(Optional)*      |Given a string value x,  |
|                          |                         |returns container names  |
|                          |                         |greater in value than    |
|                          |                         |the specified marker.    |
|                          |                         |Only strings using UTF-8 |
|                          |                         |encoding are valid.      |
+--------------------------+-------------------------+-------------------------+
|end_marker                |String *(Optional)*      |Given a string value x,  |
|                          |                         |returns container names  |
|                          |                         |lesser in value than the |
|                          |                         |specified marker. Only   |
|                          |                         |strings using UTF-8      |
|                          |                         |encoding are valid.      |
+--------------------------+-------------------------+-------------------------+
|format                    |String *(Optional)*      |Value of the serialized  |
|                          |                         |response format, either  |
|                          |                         |JSON or XML.             |
+--------------------------+-------------------------+-------------------------+
|prefix                    |String *(Optional)*      |Prefix value. Object     |
|                          |                         |names in the response    |
|                          |                         |begin with this value.   |
+--------------------------+-------------------------+-------------------------+
|delimiter                 |Char *(Optional)*        |Delimiter value, which   |
|                          |                         |returns the object names |
|                          |                         |that are nested in the   |
|                          |                         |container.               |
+--------------------------+-------------------------+-------------------------+




This operation does not accept a request body.




**Example Show account details and list containers: XML request**


.. code::

   GET /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123?format=xml HTTP/1.1
   Host: storage.clouddrive.com
   X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c





**Example Show account details and list containers: JSON request**


.. code::

   GET /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123?format=json HTTP/1.1
   Host: storage.clouddrive.com
   X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c





Response
""""""""""""""""


This table shows the header parameters for the response:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|Content-Length            |String *(Required)*      |The length of the        |
|                          |                         |response body that       |
|                          |                         |contains the list of     |
|                          |                         |names. If the operation  |
|                          |                         |fails, this value is the |
|                          |                         |length of the error text |
|                          |                         |in the response body.    |
+--------------------------+-------------------------+-------------------------+
|Content-Type              |String *(Required)*      |The MIME type of the     |
|                          |                         |list of names. If the    |
|                          |                         |operation fails, this    |
|                          |                         |value is the MIME type   |
|                          |                         |of the error text in the |
|                          |                         |response body.           |
+--------------------------+-------------------------+-------------------------+
|X-Account-Object-Count    |Int *(Required)*         |The number of objects in |
|                          |                         |the account.             |
+--------------------------+-------------------------+-------------------------+
|X-Account-Bytes-Used      |Int *(Required)*         |The total number of      |
|                          |                         |bytes that are stored in |
|                          |                         |Cloud Files for the      |
|                          |                         |account.                 |
+--------------------------+-------------------------+-------------------------+
|X-Account-Container-Count |Int *(Required)*         |The number of containers.|
+--------------------------+-------------------------+-------------------------+
|X-Account-Meta-name       |String *(Optional)*      |The custom account       |
|                          |                         |metadata item,           |
|                          |                         |where``name`` is the     |
|                          |                         |name of the metadata     |
|                          |                         |item. One ``X-Account-   |
|                          |                         |Meta-name`` response     |
|                          |                         |header appears for each  |
|                          |                         |metadata item (for       |
|                          |                         |each``name``).           |
+--------------------------+-------------------------+-------------------------+
|X-Account-Meta-Temp-URL-  |String *(Optional)*      |The secret key value for |
|Key                       |                         |temporary URLs. If not   |
|                          |                         |set, this header is not  |
|                          |                         |returned by this         |
|                          |                         |operation.               |
+--------------------------+-------------------------+-------------------------+
|X-Account-Meta-Temp-URL-  |String *(Optional)*      |A second secret key      |
|Key-2                     |                         |value for temporary      |
|                          |                         |URLs. If not set, this   |
|                          |                         |header is not returned   |
|                          |                         |by this operation.       |
+--------------------------+-------------------------+-------------------------+
|X-Trans-Id                |Uuid *(Required)*        |A unique transaction     |
|                          |                         |identifier for this      |
|                          |                         |request.                 |
+--------------------------+-------------------------+-------------------------+
|Date                      |Datetime *(Required)*    |The transaction date and |
|                          |                         |time.                    |
+--------------------------+-------------------------+-------------------------+










**Example Show account details and list containers: XML response**


.. code::

   HTTP/1.1 200 OK
   Content-Length: 262
   X-Account-Object-Count: 1
   X-Timestamp: 1389453423.35964
   X-Account-Meta-Subject: Literature
   X-Account-Bytes-Used: 14
   X-Account-Container-Count: 2
   Content-Type: application/xml; charset=utf-8
   Accept-Ranges: bytes
   X-Trans-Id: tx69f60bc9f7634a01988e6-0052d9544b
   Date: Fri, 17 Jan 2014 16:03:23 GMT
   
   <?xml version="1.0" encoding="UTF-8"?>
   <account name="my_account">
       <container>
           <name>janeausten</name>
           <count>0</count>
           <bytes>0</bytes>
       </container>
       <container>
           <name>marktwain</name>
           <count>1</count>
           <bytes>14</bytes>
       </container>
   </account>





**Example Show account details and list containers: JSON response**


.. code::

   HTTP/1.1 200 OK
   Content-Length: 96
   X-Account-Object-Count: 1
   X-Timestamp: 1389453423.35964
   X-Account-Meta-Subject: Literature
   X-Account-Bytes-Used: 14
   X-Account-Container-Count: 2
   Content-Type: application/json; charset=utf-8
   Accept-Ranges: bytes
   X-Trans-Id: tx274a77a8975c4a66aeb24-0052d95365
   Date: Fri, 17 Jan 2014 15:59:33 GMT
   
   [
      {
        "count": 0,
        "bytes": 0,
        "name": "janeausten"
      },
      {
        "count": 1,
        "bytes": 14,
        "name": "marktwain"
      }
   ]




