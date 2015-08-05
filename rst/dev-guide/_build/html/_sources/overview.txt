========
Overview
========

Rackspace Cloud Files™ is an affordable, redundant, scalable, and
dynamic storage service. The core storage system is designed to provide
a secure, network-accessible way to store an unlimited number of files.
Each file can be as large as 5 gigabytes. You can store as much as you
want and pay only for storage space that you actually use.

Cloud Files also provides a simple yet powerful way to publish and
distribute content behind a content delivery network (CDN). As a Cloud
Files user, you get access to this network automatically.

Cloud Files enables you to store and retrieve files and CDN-enabled
content through a RESTful (Representational State Transfer) web services
interface. There are also language-specific application programming
interfaces (APIs) that use the RESTful API and make it easy for
developers to integrate into their applications.

For more details about the Cloud Files service, see
http://www.rackspace.com/cloud/files/ and the Knowledge Center article
`Best Practices for Using Cloud Files <http://www.rackspace.com/knowledge_center/article/best-practices-for-using-cloud-files>`_.

Rackspace welcomes feedback, comments, and bug reports at
support@rackspacecloud.com.

=================
Intended audience
=================

This guide is intended to assist software developers who want to develop
applications using the Rackspace Cloud Files API. It fully documents the
REST application programming interface (API) that allows developers to
interact with the storage and CDN components of the Cloud Files system.
To use the information provided here, you must first have a general
understanding of the Rackspace Cloud Files service and have access to an
active Rackspace Cloud Files account. You should also be familiar with
the following items:

-  RESTful web services

-  HTTP/1.1

System administrators and others interested in the storage and CDN
benefits of Cloud Files should consider using the File Manager interface
within the Rackspace Cloud Control Panel, `Jungle
Disk <http://www.jungledisk.com/>`__, or third-party tools such as
`Cyberduck <http://www.cyberduck.ch/>`__. The Rackspace Cloud Control
Panel provides an easy to use web-based interface for uploading content
to and downloading content from Cloud Files.

Rackspace also provides language-specific APIs in several popular programming languages. Customers who are interested in accessing Cloud Files by using one of the language-specific APIs should see `developer.rackspace.com <http://developer.rackspace.com/>`_.

=======================
Document change history
=======================

This version of the guide replaces and obsoletes all earlier versions.
The most recent changes are described in the following table:

+----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Revision Date  |         Summary of Changes                                                                                                                                  |
+================+=============================================================================================================================================================+
| May 1, 2015    |- Updated "Create or update object metadata" to remove the sentence "You cannot use this operation to change other headers, such as Content-Type.".          |
+----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
| April 23, 2015 |- Corrected links in "Assigning roles to account users".                                                                                                     |
+----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
| March 23, 2015 |- Corrected the URI in the table in “CDN object services” to include the container information and added a warning with information to make sure that you are|
|                |  using the CDN management services URIs for this DELETE operation.                                                                                          |
|                |                                                                                                                                                             |
|                |- Corrected the URI in "Delete CDN-enabled object" to include the container information|and added additional information to this operation description       |
|                |  with updated request and response examples.                                                                                                                |
+----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+

====================
Additional resources
====================
You can download the most current versions of Rackspace API documentation at 
`developer.rackspace.com <http://developer.rackspace.com/docs>`_.

For more details about the Cloud Files service, see
http://www.rackspace.com/cloud/files/. Related documents are available
at the same site, as are links to official Rackspace support channels,
including Knowledge Center articles, forums, phone, chat, and email.

For information about the Rackspace language-specific APIs that you can
use for Cloud Files, see `SDKs & Tools <https://developer.rackspace.com/sdks/>`__.
Each language-specific API includes its own documentation (either HTML,
PDF, or CHM) including code snippets and examples to help you get
started.

=========================
Pricing and service level
=========================

Cloud Files is part of the Rackspace Cloud and your use of it through
the API is billed according to the pricing schedule at
`www.rackspace.com/cloud/public/files/pricing <http://www.rackspace.com/cloud/public/files/pricing/>`__.

The service level agreement (SLA) for Cloud Files is available at `Cloud
Files
SLA <http://www.rackspace.com/information/legal/cloud/sla?page=files#cloud_files_sla>`__.

