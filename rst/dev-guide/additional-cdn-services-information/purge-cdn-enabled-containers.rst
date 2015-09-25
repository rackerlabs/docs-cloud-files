.. _purge-cdn-enabled-containers:

Purge CDN-enabled containers
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For a container to be purged from the CDN, you can either wait for the
TTL to expire, or you can request that Rackspace remove, or purge, a
CDN-enabled container from the network. After you have made the request
to Rackspace through a support ticket, the system purges the container
from the CDN, and sends an email to the address (or multiple addresses)
that you indicate through the ticket. The email address notification is
optional.


.. note::
   To prevent the container from going back to the CDN, first change the
   ``X-CDN-Enabled`` flag to ``False`` as described in the operation to CDN-enable and CDN-disable a container at `Cloud Files API v1 <http://api.rackspace.com/api-ref-files.html>`__.
