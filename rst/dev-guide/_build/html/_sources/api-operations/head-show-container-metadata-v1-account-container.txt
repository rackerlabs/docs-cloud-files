
.. THIS OUTPUT IS GENERATED FROM THE WADL. DO NOT EDIT.

Show container metadata
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    HEAD /v1/{account}/{container}

Shows container metadata, including the number of objects in the container and the total bytes for all objects stored in the container.

Use a ``HEAD`` operation against the container to return the following metadata: 



*  How many objects are in the container ( ``X-Container-Object-Count`` )
*  The total bytes for all objects stored in the container ( ``X-Container-Bytes-Used`` )
*  Any custom metadata that is set on the container ( ``X-Container-Meta-name`` )


To set and edit your custom metadata, see `Create or update container metadata <http://docs.rackspace.com/files/api/v1/cf-devguide/content/POST_updateacontainermeta_v1__account___container__containerServicesOperations_d1e000.html>`__.

If the container exists, a status code of 200 through 299 is returned. If the container does not exist, a status code of 404 (Not Found) is returned.

This operation does not require a request body and does not return a response body.



This table shows the possible response codes for this operation:


+--------------+--------+-----------------------------------------------------------+
|Response Code |Name    |Description                                                |
+==============+========+===========================================================+
|204           |No      |The request succeeded. The server fulfilled the request    |
|              |Content |but does not need to return a body.The number of objects   |
|              |        |in the container. The total number of bytes used for all   |
|              |        |objects in the container.Any metadata set on the           |
|              |        |container. The ``name`` at the end of the header is the    |
|              |        |name of your metadata. One ``X-Container-Meta-name``       |
|              |        |response header appears for each metadata item (for each   |
|              |        |``name``).An internal variable that indicates the last     |
|              |        |time an entity (account, container, or object) was         |
|              |        |modified. The format is the same as a Unix timestamp. The  |
|              |        |storage system uses this header to determine the latest    |
|              |        |version. For example, during replication, the storage      |
|              |        |system makes sure all three object replicas are up to      |
|              |        |date, and it uses the X-Timestamp header to determine      |
|              |        |which replica is the latest. You might notice that objects |
|              |        |have both a Last-Modified and X-Timestamp header. The      |
|              |        |difference between these two headers is the resolution.    |
|              |        |Last-Modified has resolution up to one second, while X-    |
|              |        |Timestamp has resolution up to five decimal places of one  |
|              |        |second.The access control list (ACL) that grants read      |
|              |        |access. If not set, this header is not returned by this    |
|              |        |operation. This header can contain a comma-delimited list  |
|              |        |of users that can read the container (allows the GET       |
|              |        |method for all objects in the container).The ACL that      |
|              |        |grants write access. If not set, this header is not        |
|              |        |returned by this operation. This header can contain a      |
|              |        |comma-delimited list of users that can write to the        |
|              |        |container (allows PUT, POST, COPY, and DELETE methods for  |
|              |        |all objects in the container).The length of the response   |
|              |        |body that contains the list of names. If the operation     |
|              |        |fails, this value is the length of the error text in the   |
|              |        |response body.The MIME type of the list of names. If the   |
|              |        |operation fails, this value is the MIME type of the error  |
|              |        |text in the response body.A unique transaction identifier  |
|              |        |for this request.The transaction date and time.The type of |
|              |        |ranges accepted. Sets the secret key for container         |
|              |        |synchronization. For container synchronization, you must   |
|              |        |set ``X-Container-Sync-Key`` on the source container and   |
|              |        |the destination container.Sets the destination for         |
|              |        |container synchronization. For container synchronization,  |
|              |        |the ``X-Container-Sync-To`` value must follow the form     |
|              |        |//realmName/clusterName/accountName/containerName.Enables  |
|              |        |versioning on this container. The value is the name of     |
|              |        |another container. You must UTF-8-encode and then URL-     |
|              |        |encode the name before you include it in the header. To    |
|              |        |disable versioning, set the header to an empty string.     |
+--------------+--------+-----------------------------------------------------------+
|404           |Not     |The requested resource was not found.                      |
|              |Found   |                                                           |
+--------------+--------+-----------------------------------------------------------+


Request
""""""""""""""""


This table shows the header parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|X-Auth-Token              |String *(Required)*      |Authentication token.    |
+--------------------------+-------------------------+-------------------------+




This table shows the URI parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|{account}                 |String                   |Your unique account      |
|                          |                         |identifier.              |
+--------------------------+-------------------------+-------------------------+
|{container}               |String                   |The unique identifier of |
|                          |                         |the container.           |
+--------------------------+-------------------------+-------------------------+





This operation does not accept a request body.




**Example Get container metadata: HTTP request**


.. code::

    HEAD /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer HTTP/1.1
    Host: storage.clouddrive.com
    X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c
    


Response
""""""""""""""""


This table shows the header parameters for the response:

+------------+-------------+---------------------------------------------------+
|Name        |Type         |Description                                        |
+============+=============+===================================================+
|X-Container-|Int          |The number of objects in the container.            |
|Object-Count|*(Required)* |                                                   |
+------------+-------------+---------------------------------------------------+
|X-Container-|Int          |The total number of bytes used for all objects in  |
|Bytes-Used  |*(Required)* |the container.                                     |
+------------+-------------+---------------------------------------------------+
|X-Container-|String       |Any metadata set on the container. The ``name`` at |
|Meta-name   |*(Required)* |the end of the header is the name of your          |
|            |             |metadata. One ``X-Container-Meta-name`` response   |
|            |             |header appears for each metadata item (for each    |
|            |             |``name``).                                         |
+------------+-------------+---------------------------------------------------+
|X-Timestamp |String       |An internal variable that indicates the last time  |
|            |*(Required)* |an entity (account, container, or object) was      |
|            |             |modified. The format is the same as a Unix         |
|            |             |timestamp. The storage system uses this header to  |
|            |             |determine the latest version. For example, during  |
|            |             |replication, the storage system makes sure all     |
|            |             |three object replicas are up to date, and it uses  |
|            |             |the X-Timestamp header to determine which replica  |
|            |             |is the latest. You might notice that objects have  |
|            |             |both a Last-Modified and X-Timestamp header. The   |
|            |             |difference between these two headers is the        |
|            |             |resolution. Last-Modified has resolution up to one |
|            |             |second, while X-Timestamp has resolution up to     |
|            |             |five decimal places of one second.                 |
+------------+-------------+---------------------------------------------------+
|X-Container-|String       |The access control list (ACL) that grants read     |
|Read        |*(Optional)* |access. If not set, this header is not returned by |
|            |             |this operation. This header can contain a comma-   |
|            |             |delimited list of users that can read the          |
|            |             |container (allows the GET method for all objects   |
|            |             |in the container).                                 |
+------------+-------------+---------------------------------------------------+
|X-Container-|String       |The ACL that grants write access. If not set, this |
|Write       |*(Optional)* |header is not returned by this operation. This     |
|            |             |header can contain a comma-delimited list of users |
|            |             |that can write to the container (allows PUT, POST, |
|            |             |COPY, and DELETE methods for all objects in the    |
|            |             |container).                                        |
+------------+-------------+---------------------------------------------------+
|Content-    |String       |The length of the response body that contains the  |
|Length      |*(Required)* |list of names. If the operation fails, this value  |
|            |             |is the length of the error text in the response    |
|            |             |body.                                              |
+------------+-------------+---------------------------------------------------+
|Content-Type|String       |The MIME type of the list of names. If the         |
|            |*(Required)* |operation fails, this value is the MIME type of    |
|            |             |the error text in the response body.               |
+------------+-------------+---------------------------------------------------+
|X-Trans-Id  |Uuid         |A unique transaction identifier for this request.  |
|            |*(Required)* |                                                   |
+------------+-------------+---------------------------------------------------+
|Date        |Datetime     |The transaction date and time.                     |
|            |*(Required)* |                                                   |
+------------+-------------+---------------------------------------------------+
|Accept-     |String       |The type of ranges accepted.                       |
|Ranges      |*(Required)* |                                                   |
+------------+-------------+---------------------------------------------------+
|X-Container-|String       |Sets the secret key for container synchronization. |
|Sync-Key    |*(Optional)* |For container synchronization, you must set ``X-   |
|            |             |Container-Sync-Key`` on the source container and   |
|            |             |the destination container.                         |
+------------+-------------+---------------------------------------------------+
|X-Container-|String       |Sets the destination for container                 |
|Sync-To     |*(Optional)* |synchronization. For container synchronization,    |
|            |             |the ``X-Container-Sync-To`` value must follow the  |
|            |             |form                                               |
|            |             |//realmName/clusterName/accountName/containerName. |
+------------+-------------+---------------------------------------------------+
|X-Versions- |String       |Enables versioning on this container. The value is |
|Location    |*(Optional)* |the name of another container. You must UTF-8-     |
|            |             |encode and then URL-encode the name before you     |
|            |             |include it in the header. To disable versioning,   |
|            |             |set the header to an empty string.                 |
+------------+-------------+---------------------------------------------------+







**Example Get container metadata: HTTP response**


.. code::

    HTTP/1.1 204 No Content
    Content-Length: 0
    X-Container-Object-Count: 1
    Accept-Ranges: bytes
    X-Container-Meta-Book: TomSawyer
    X-Timestamp: 1389727543.65372
    X-Container-Meta-Author: SamuelClemens
    X-Container-Bytes-Used: 14
    Content-Type: text/plain; charset=utf-8
    X-Trans-Id: tx0287b982a268461b9ec14-0052d826e2
    Date: Thu, 16 Jan 2014 18:37:22 GMT


