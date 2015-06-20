===================================
Additional CDN services information
===================================

The section provides additional information about working with the Cloud
Files CDN services.

Purge CDN-enabled containers
----------------------------

For a container to be purged from the CDN, you can either wait for the
TTL to expire, or you can request that Rackspace remove, or purge, a
CDN-enabled container from the network. After you have made the request
to Rackspace through a support ticket, the system purges the container
from the CDN, and sends an email to the address (or multiple addresses)
that you indicate through the ticket. The email address notification is
optional.


.. note::
   To prevent the container from going back to the CDN, first change the
   ``X-CDN-Enabled`` flag to ``False`` as shown in the section about
   CDN-enabling and disabling a container.
