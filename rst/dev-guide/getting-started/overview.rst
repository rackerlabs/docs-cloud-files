.. _gsg-overview:

===============================
Overview
===============================

Rackspace Cloud Files™ is an affordable, redundant, scalable, and
dynamic storage service. The core storage system is designed to provide
a secure, network-accessible way to store an unlimited number of files.
Files that exceed 5 GBs in size are broken down into 5 GB (or less)
segments. For example, if you need to store large files, such as videos,
HD movies, or backups, Cloud Files accomplishes this by enabling you to
upload multiple file segments and a manifest file to map those segments
together. Large files are then downloaded as a single file. You can
store as much as you want and pay only for storage space that you
actually use.

Cloud Files also provides a simple yet powerful way to publish and
distribute content behind a content delivery network (CDN). As a Cloud
Files user, you get access to this network automatically.

Cloud Files enables you to store and retrieve files and CDN-enabled
content through a simple RESTful (Representational State Transfer) web
services interface. There are also language-specific application
programming interfaces (APIs) that use the RESTful API and make it easy
for developers to integrate Cloud Files into their applications.

The following diagram illustrates the various system interfaces and how
content can be distributed over the CDN. The process is straightforward:
authenticate, create a container, upload objects, mark the container as
public, and begin serving that content from a powerful CDN.

..  note:: 
    Marking the container as public means enabling the container to be
    distributed over the CDN. A CDN-enabled container is publicly
    accessible. 

For more details about the Cloud Files service, see
http://www.rackspace.com/cloud/files/ and the Knowledge Center article
`Best Practices for Using Cloud
Files <http://www.rackspace.com/knowledge_center/article/best-practices-for-using-cloud-files>`__.

Rackspace welcomes feedback, comments, and bug reports at
support@rackspacecloud.com.

This guide provides step-by-step instructions to enter the necessary
URLs or commands to use basic Cloud Files API operations. You can find
details about advanced Cloud Files functionality, such as dynamic large
objects, static large objects, TempURLs, and FormPOST, in the :ref:`API reference <api-reference>`.

This guide uses the API directly with cURL (:ref:`Using the API directly by
using cURL <gsg-using-curl>`).
