==========================
Overview of API operations
==========================

The Cloud Files API is implemented as a set of RESTful web services. All 
authentication and container/object operations can be performed with standard 
HTTP calls. For more information about REST, see 
`Representation State Transfer <https://en.wikipedia.org/wiki/Representational_state_transfer>`__.

The following constraints apply to REST API HTTP requests:

- Maximum number of HTTP headers per request: 90

- Maximum length of all HTTP headers: 4096 bytes

- Maximum length per HTTP request line: 8192 bytes

- Maximum length of HTTP request: 5 gigabytes

- Maximum length of container name: 256 bytes

- Maximum length of object name: 1024 bytes

Container and object names must be UTF-8 encoded and then URL-encoded before 
interacting with the REST interface. You might be using an API binding that 
performs the URL-encoding on your behalf. If so, do not URL-encode before 
calling the API binding, or you will double-encode container and object names. 
Check the length restrictions against the URL-encoded string.

.. note::
   The language-specific APIs handle URL-encoding and decoding.

Each REST request against Cloud Files requires the inclusion of an authorization 
token in the ``X-Auth-Token`` header. You obtain this token, along with the Cloud
Files URIs, by first using the Rackspace authentication service and supplying a 
valid user name and API access key. For more information, see :ref:`Authentication<auth>`.

The following services make up the full Cloud Files product :

- **Storage service**: The service identified with cloudFiles in the service catalog manages the data storage in the system. Example operations are creating containers and uploading objects.

- **CDN management service**: The service identified with cloudFilesCDN in the service catalog manages the CDN feature of Cloud Files.

The purpose of each HTTP method depends on which
service the call is made against. For example, a PUT request against one of the 
cloudFiles endpoints can be used to create a container or upload an object, 
while a PUT request against the one of the cloudFilesCDN endpoints is used to 
CDN-enable a container.

The language-specific APIs mask this system separation. They simply create a 
container and mark it public and handle calling the appropriate back-end 
services by using the appropriate REST APIs.

.. note::
   All requests to authenticate and operate against Cloud Files are performed using SSL over HTTP (HTTPS) on TCP port 443.

The following diagram illustrates the various system interfaces and the ease 
with which content can be distributed over the CDN. The process is simple: 
authenticate, create a container, upload objects, mark the container as public, 
and begin serving that content from a powerful CDN.

.. note::
   Marking the container as public simply means enabling the container to be distributed over the CDN. A CDN-enabled container is publicly accessible.

.. image:: /_images/CFinterfaces_New.png