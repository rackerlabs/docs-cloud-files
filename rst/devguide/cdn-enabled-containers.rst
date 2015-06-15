======================
CDN-enabled containers
======================

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

