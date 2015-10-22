.. _concepts:

Concepts
---------

Cloud Files is not a file system in the traditional sense. You cannot
map or mount virtual disk drives like you can with other forms of
storage such as a SAN or NAS. Because Cloud Files is a different kind of
storage system, you should review the following key terms and
concepts..

Accounts
~~~~~~~~

The Cloud Files system is designed to be used by many different
customers. Your user account is your portion of the Cloud Files system.
You must identify yourself with your Rackspace Cloud user name and API
access key. After you are authenticated, you have full read/write access
to the files stored under your account. To obtain a Cloud Files account
and enable your API access key, go to
`http://www.rackspacecloud.com/signup <https://cart.rackspace.com/cloud/?cp_id=cloud_files>`__.

Authentication
~~~~~~~~~~~~~~

The Cloud Identity Guide describes how to authenticate against the Rackspace 
Cloud Identity service to receive Cloud Files connection parameters and an
authentication token. The token must be passed to Cloud Files operations
during the time that it is valid.

For more information about authentication, see the :rax-devguide:`Cloud Identity Client Developer Guide <cloud-identity/v2>`.

.. note::
   The language-specific APIs handle authentication, token passing, and
   HTTPS request/response communication.

Permissions
~~~~~~~~~~~

In Cloud Files, you have your own storage account and full access to that 
account. You must authenticate with your credentials as described in :ref:`the 
section on authentication <auth>`. After you are authenticated, you can 
perform all Cloud Files operations within that account.

You can use Role Based Access Control (RBAC) with Cloud Files. For more 
information, see :ref:`Role Based Access Control <rbac>`.

Containers
~~~~~~~~~~

A container is a storage compartment that provides a way for you to organize 
your data. You can think of a container like a folder in Windows® or a directory
in UNIX®. The primary difference between a container and these other file
system concepts is that containers cannot be nested. You can have up to 500,000
containers in your account. Data must be stored in a container, so you must
have at least one container defined in your account before you upload data.

If you expect to write more than 100 objects per second to a single container, 
we recommend organizing those objects across multiple containers to improve 
performance.

The only restrictions on container names is that they cannot contain a forward 
slash (/) and must be less than 256 bytes in length. Note that the length 
restriction applies to the name after it has been URL-encoded. For example, a 
container name of Course Docs would be URL-encoded as Course%20Docs and is 
therefore 13 bytes in length rather than the expected 11.

You can create a container in any Rackspace data center. (See 
:ref:`Service access endpoints <service-access>` for a list.) However,
in order to lower your costs, you should create your most served containers in 
the same data center as your server. Otherwise, you will be billed for external 
bandwidth charges. Note that this is true when computations are performed on 
objects but is not true for static content served to end users directly.

In addition to containing objects, you can also use the container to control 
access to objects by using an access control list (ACL). For more information, 
see :ref:`Container access control lists <container-acls>`. You cannot
store an ACL with individual objects.

Objects
~~~~~~~

Objects are the basic storage entities in Cloud Files. They represent
the files and their optional metadata that you upload to the system.
When you upload objects to Cloud Files, the data is stored as-is
(without compression or encryption) and consists of a location
(container), the object's name, and any metadata that you assign,
consisting of key/value pairs. For example, you can choose to store a
backup of your digital photos and organize them into albums. In this
case, each object could be tagged with metadata such as
``Album : Caribbean Cruise`` or ``Album : Aspen Ski Trip``.

The only restriction on object names is that they must be less than 1024
bytes in length after URL-encoding. For example, an object name of
``C++final(v2).txt`` would be URL-encoded as
``C%2B%2Bfinal%28v2%29.txt`` and therefore is 24 bytes in length rather
than the expected 16.

Cloud Files limits the size of a single uploaded object. By default this
limit is 5 GB. However, the download size of a single object is
virtually unlimited with the use of segmentation. Segments of the larger
object are uploaded and a special manifest file is created that, when
downloaded, sends all the segments concatenated as a single object.
Segmentation also offers much greater upload speed with the possibility
of parallel uploads of the segments.

For metadata, do not exceed 90 individual key/value pairs for any one
object and do not exceed 4 KB (4096 bytes) for the total byte length of
all key/value pairs.

Operations
~~~~~~~~~~

Operations are the actions you perform within your account, such as
creating or deleting containers or uploading or downloading objects. For 
information about the Cloud Files API operations, see :ref:`API reference 
<api-reference>`.

You can perform operations through the REST web service API or a
language-specific API. For information about the Rackspace
language-specific APIs, see :rax-dev:`SDKs and tools<sdks>`.

.. note::
   All operations must include a valid authorization token.

CDN-enabled containers
~~~~~~~~~~~~~~~~~~~~~~

CDN-enabled containers serve content through the Akamai content delivery
network (CDN). CDN-enabled containers are publicly accessible for read
access, so they do not require an authorization token for read access.
However, uploading content into a CDN-enabled container is a secure
operation and requires a valid authentication token.

Each CDN-enabled container has a unique URI that can be combined with
its object names and openly distributed in web pages, emails, or other
applications.

For example, a CDN-enabled container named ``photos`` might be
referenced as
``http://80745c48926cd286a5a0-48261ebe0e4c795a565ece6b9cca2fe8.r10.cf1.rackcdn.com``.
If that container houses ashot called ``wow1.jpg``, that image
can be served by a CDN with the full URL of
``http://80745c48926cd286a5a0-48261ebe0e4c795a565ece6b9cca2fe8.r10.cf1.rackcdn.com/wow1.jpg``.

This URI can be embedded in items like HTML pages, email messages, or
blog posts. The first time that the URI is accessed, a copy of that
image is fetched from the Cloud Files storage system. The copy is cached
in a CDN and served from there for all subsequent requests for a
configurable cache time to live (TTL) value. Setting the TTL of a
CDN-enabled container translates to setting the ``Expires`` and
``Cache-Control`` HTTP headers. Note that extremely long TTL values do
not guarantee that an object is served from a CDN edge location. When
the TTL expires, the CDN checks Cloud Files to ensure that it has the
most up-to-date content. A purge request forces the CDN to check with
Cloud Files for the most up-to-date version of the file.

Cloud Files continues to serve content through the CDN until it receives
a delete request.

Containers tracked in the CDN management service are completely separate
and distinct from the containers defined in the storage service. It is
possible for a container to be CDN-enabled even if it does not exist in
the storage system. You might want the ability to pre-generate CDN URLs
before actually uploading content, and this separation gives you that
ability.

However, for the content to be served from the CDN, the container names
**must** match in both the CDN management service and the storage
service. For example, you could CDN-enable a container called ``images``
and be assigned the CDN URI, but you also need to create a container
called ``images`` in the storage service.

For more information about CDN-enabled containers and operations for them, see :ref:`API operations for CDN services <api-operations-for-cdn-services>`.

Language-specific APIs
~~~~~~~~~~~~~~~~~~~~~~

APIs in several popular languages are available to help put Cloud Files
in the hands of developers. These language-specific APIs provide a layer
of abstraction on top of the base REST API, enabling developers to work
with a container and object model instead of working directly with HTTP
requests and responses. The language-specific APIs are available at no
cost to download, use, and modify. They are licensed under the MIT
license as described in the COPYING file packaged with each API.

If you make any improvements to a Cloud File language-specific API, you
are encouraged (but not required) to submit those changes back to
Rackspace. If you want to suggest changes to an API, send an email to
sdk-support@rackspace.com. Be sure to indicate which language and
version you modified and send a unified ``diff``.

Detailed information about the language-specific APIs is in the
Rackspace Cloud SDKs Software Development Kit Guide. Each API has its
own documentation (in HTML, PDF, or CHM format) including code snippets
and examples to help you get started.

You are welcome to create your own language-specific APIs. Rackspace
will help answer any questions during development, host your code if you
like, and give you full credit for your work.

For more information about the Rackspace SDKs, see :rax-dev:`SDKs and tools<sdks>`.


