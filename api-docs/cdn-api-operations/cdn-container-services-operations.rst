.. cdn-container-services-operations:

CDN container services operations
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can perform the operations described in the section on CDN-enabled containers in your Cloud Files account.

When you CDN-enable a container, all the objects within it become available on the CDN. Similarly, after a container is CDN-enabled, any objects added to it through the storage service become CDN-enabled. After you CDN-enable a container, its publicly-available URI can be found with the header X-Cdn-Uri, and its objects can be accessed with X-Cdn-Uri/objectName. By knowing this pattern, you can pre-generate the URI for an object before it is added to the container.

When you enable a container in the CDN service, you automatically generate URIs for SSL and streaming usage. They are listed under the X-Cdn-Ssl-Uri and X-Cdn-Streaming-Uri headers.

On August 13, 2012, the format of new CDN URIs changed in order to enhance the security of the CDN. Any URIs set in the older format (for example, http://c25810.r10.cf1.rackcdn.com/mydog.jpg) continue to work. However, any newly generated CDN URIs have the new format, as shown in the following example: http://80745c48926cd286a5a0-48261ebe0e4c795a565ece6b9cca2fe8.r10.cf1.rackcdn.com/mydog.jpg. 

.. note::
   Monitor your CDN charges. When you CDN-enable a container, not only can anyone view it,
   but anyone can link to it. We recommend that you monitor your bandwidth usage and 
   charges in the Cloud Control Panel so that you know if someone is hot-linking your 
   content. For instructions about viewing your usage charges, see 
   :how-to:`Protect your Cloud Files CDN Bill from Unexpected Usage<protect-your-cloud-files-cdn-bill-from-unexpected-usage>`. 

The examples in this section use sample values for the following:

- account — for example, MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123

- X-Auth-Token — for example, f064c46a782c444cb4ba4b6434288f7c

- container — for example, MyContainer

For your own requests, you must use your own account information, authentication token, and container names. (For more information, see the authentication section.) Your authentication token and your account information are in the service catalog that is produced.
   
.. include:: methods/put-cdn-enable-and-cdn-disable-a-container-v1-account-container.rst
.. include:: methods/head-list-metadata-for-cdn-enabled-container-v1-account-container.rst
.. include:: methods/post-update-cdn-enabled-container-metadata-v1-account-container.rst