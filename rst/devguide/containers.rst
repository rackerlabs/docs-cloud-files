==========
Containers
==========

A container is a storage compartment that provides a way for you to
organize your data. You can think of a container like a folder in
Windows® or a directory in UNIX®. The primary difference between a
container and these other file system concepts is that containers cannot
be nested. You can have up to 500,000 containers in your account. Data
must be stored in a container, so you must have at least one container
defined in your account before you upload data.

If you expect to write more than 100 objects per second to a single
container, we recommend organizing those objects across multiple
containers to improve performance.

The only restrictions on container names is that they cannot contain a
forward slash (``/``) and must be less than 256 bytes in length. Note
that the length restriction applies to the name after it has been
URL-encoded. For example, a container name of ``Course Docs`` would be
URL-encoded as ``Course%20Docs`` and is therefore 13 bytes in length
rather than the expected 11.

You can create a container in any Rackspace data center. (See `???`
for a list.) However, in order to lower your costs, you should create
your most served containers in the same data center as your server.
Otherwise, you will be billed for external bandwidth charges. Note that
this is true when computations are performed on objects but is not true
for static content served to end users directly.

In addition to containing objects, you can also use the container to
control access to objects by using an access control list (ACL). For
more information, see `Public access to your Cloud Files account <public-access-to-your-cloud-files-account>`_. You cannot store an ACL
with individual objects.
