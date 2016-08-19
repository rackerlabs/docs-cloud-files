.. _account-to-account_copy:

Account to account copy
~~~~~~~~~~~~~~~~~~~~~~~

The account to account copy capability adds the ability to copy objects
between different accounts on the server.

To use this capability to read from or write to the accounts, you must
have a access to the containers. You can use a container access control
list (ACL) to control access to a container and its objects.

Use the following operations and headers to perform an account to
account copy:

-  A **COPY** command with the following headers:

   -  ``Destination-Account``: Specifies the account name (which
      corresponds to the last part of the storage URL).

   -  ``Destination``: Used with **COPY**, specifies the container and
      object name of the destination object in the form of
      ``/container/object``.

-  A **PUT** command with the following headers:

   -  ``X-Copy-From-Account``: Specifies the account name (which
      corresponds to the last part of storage URL).

   -  ``X-Copy-From``: Used with **PUT**, specifies the container and
      object name of the source object in the form of
      ``/container/object``.

.. note:: If your storage URL is
   ``https://storage101.dfw1.clouddrive.com/v1/
   MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee``,
   your account name is
   ``MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee``.

Use the following examples to complete the steps to use account to
account copy.

**COPY command steps**

1. Use the **POST** command to set ``X-Container-Write`` metadata on the
   destination container.

   **Request:**

   .. code::

       POST /v1/Destination_Account/Destination_Container HTTP/1.1
       Host: storage.clouddrive.com
       X-Auth-Token: Destination_User_Auth_Token
       X-Container-Write: Source_User_Name

   **Response:**

   .. code::

       204 No Content
       Content-Length: 0
       Content-Type: text/html; charset=UTF-8
       X-Trans-Id: tx1abc1d6005134be99b1db-0054da619adev1
       Date: Tue, 10 Feb 2015 19:52:58 GMT

2. Use the **COPY** command to copy the object.

   **Request:**

   .. code::

       COPY /v1/Source_Account/Source_Destination/Source_Object HTTP/1.1
       Host: storage.clouddrive.com
       X-Auth-Token: Source_User_Auth_Token
       Destination: Destination_Container/Destination_Object
       Destination-Account: Destination_User_Account   (such as, MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee)

   **Response:**

   .. code::

       201 Created
       Content-Length: 0
       X-Copied-From-Last-Modified: Tue, 13 Jan 2015 20:53:09 GMT
       X-Copied-From: copy_test/new_copy_object.txt
       Last-Modified: Tue, 10 Feb 2015 19:59:49 GMT
       Etag: c6995201745ed71f24ba352750bde444
       X-Copied-From-Account: StagingUS_xxxxxxxx-yyyy-zzzz-aaaa-bbbbbbbbbbbb
       Content-Type: text/html; charset=UTF-8
       X-Trans-Id: txd819a3f557de449cb0879-0054da6334dev1
       Date: Tue, 10 Feb 2015 19:59:48 GMT


**PUT command steps**

1. Use the POST command to set ``X-Container-Write`` metadata on
   destination container.

   **Request:**

   .. code::

       POST  /v1/Destination_Account/Destination_Container HTTP/1.1
       Host: storage.clouddrive.com
       X-Auth-Token: Destination_User_Auth_Token
       X-Container-Write: Source_User_Name

   **Response:**

   .. code::

       204 No Content
       Content-Length: 0
       Content-Type: text/html; charset=UTF-8
       X-Trans-Id: tx0f6c102033564bb0800e3-0054da677fdev1
       Date: Tue, 10 Feb 2015 20:18:07 GMT

2. Use the **PUT** command to copy the object.

   **Request:**

   .. code::

       PUT  /v1/Destination_Account/Dest_Container/Dest_Object HTTP/1.1
       Host: storage.clouddrive.com
       X-Auth-Token: Source_User_Auth_Token
       X-Copy-From: /source_container/source_object
       X-Copy-From-Account: Source_User_Account   (such as, MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee)
       Content-Length: 0      (the actual value is ignored)

   **Response:**

   .. code::

       201 Created
       Content-Length: 0
       X-Copied-From-Last-Modified: Tue, 10 Feb 2015 20:46:32 GMT
       X-Copied-From: source/source_object.txt
       Last-Modified: Tue, 10 Feb 2015 21:14:50 GMT
       Etag: d41d8cd98f00b204e9800998ecf8427e
       X-Copied-From-Account: StagingUS_xxxxxxxx-yyyy-zzzz-aaaa-bbbbbbbbbbbb
       Content-Type: text/html; charset=UTF-8
       X-Trans-Id: txe3373a175f944020a63d9-0054da74c9dev1
       Date: Tue, 10 Feb 2015 21:14:49 GMT
