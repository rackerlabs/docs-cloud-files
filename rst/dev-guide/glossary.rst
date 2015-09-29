.. _glossary:

========
Glossary
========

Account
    The portion of the Cloud Files system designated for your use. The
    Cloud Files system is designed to be used by many different
    customers, and your user account is your portion of it. Your user
    account is your slice of the Cloud Files system. You must identify
    yourself with a valid user name and your API access key. After you
    are authenticated, your have full read/write access to the objects
    (files) stored under your account.

Application program interface (API)
    A set of routines, protocols, and tools for building software
    applications.

Authentication
    The process if identifying yourself to the Rackspace Cloud Identity
    service to receive Cloud Files connection parameters and an
    authentication token. While the authentication token is valid (which
    in most cases is 24 hours), you must pass it to Cloud Files to
    perform all Cloud Files operations.

CDN-enabled containers
    Containers that serve content through the Akamai content delivery
    network (CDN). When a container is CDN-enabled, any files in the
    container are publicly accessible and do not require an
    authentication token for read access. However, uploading content
    into a CDN-enabled container is a secure operation and requires a
    valid authentication token. Each published container has a unique
    URL that can be combined with its object name and openly distributed
    in web pages, emails, or other applications. For example, a
    CDN-enabled container named ``photos`` can be referenced as
    ``http://80745c48926cd286a5a0-48261ebe0e4c795a565ece6b9cca2fe8.r10.cf1.rackcdn.com``.
    If that container houses an image called ``mydog.jpg``, that image
    can be served by the Akamai CDN with the full URL of
    ``http://80745c48926cd286a5a0-48261ebe0e4c795a565ece6b9cca2fe8.r10.cf1.rackcdn.com/mydog.jpg.``.

Container
    A storage compartment that provides a way for you to organize data.
    A container is similar to a folder in Windows or a directory in
    UNIX. The primary difference between a container and these other
    file system concepts is that containers cannot be nested.

Content delivery network (CDN)
    A system of distributed servers (network) that delivers web pages
    and other web content to a user based on the geographic locations of
    the user, the origin of the web page, and a content delivery server.

Language-specific API
    APIs that provide a layer of abstraction on top of the base REST
    API, enabling programmers to work with a container and object model
    instead of working directly with HTTP requests and responses.
    Language-specific APIs in several popular languages are available
    for Cloud Files.

Metadata
    Optional information that you can assign to Cloud Files accounts,
    containers, and objects through the use of a metadata header.

Middleware
    Software that connects two otherwise separate applications. For
    example, there are a number of middleware products that link a
    database system to a web server.

Operations
    The actions you perform against your account in Cloud Files, such as
    creating or deleting containers. Operations are performed via the
    REST web service API or a language-specific API.

Private container
    A container that is only accessible by the account holder.

Pseudo directories
    A hierarchical structure within a single Cloud Files container
    created adding forward slash characters (``/``) in the object name.

Public container
    A CDN-enabled container that is publicly accessible.

REST
    REST, short for Representational State Transfer, is an architectural
    style for large-scale software design.

Segmentation
    The process of segmenting a large file into a number of smaller
    files for uploading to Cloud Files. Cloud Files limits the size of a
    single uploaded object. By default this limit is 5 GB. However, the
    download size of a single object is virtually unlimited with the use
    of segmentation. Segments of the larger object are uploaded and a
    special manifest file is created that, when downloaded, sends all
    the segments concatenated as a single object. Segmentation also
    offers much greater upload speed with the possibility of parallel
    uploads of the segments.

TTL
    Time-to-live value.
