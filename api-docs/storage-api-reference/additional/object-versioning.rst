.. _object-versioning:

Object versioning
~~~~~~~~~~~~~~~~~

Object versioning enables you to store multiple versions of your content
so that you can recover from unintended overwrites and deletions. It
provides an easy way to implement version control that can be used on
any type of content.

We strongly recommends that you put non-current objects in a separate
container from the current versions of objects. After you enable object
versioning, new data written to an object causes the last-current
version to be written to the separate container. Each of the non-current
versions has a timestamp appended to it, so you know when it was
originally created.

To enable object versioning, you perform the following steps:

#. Create a container where your non-current versions will be written.

#. On the container that holds the current versions of your objects, set
   the X-Versions-Location metadata header to point to the new
   non-current version container that you created.

After you complete these steps, versioning is enabled on each object in
your current-version container. Changes to the objects automatically
create non-current versions in the separate container.

Nothing is written to the non-current version container when you
initially use a **PUT** operation to add an object into the
current-version container. You create non-current versions only when you
edit existing objects with a **PUT** request. These non-current versions
are labeled according to the following schema:

``{length}{objectName}/{time stamp}``

Where ``{length}`` is the 3-character zero-padded hexadecimal character
length of the ``{objectName}``, and ``{timestamp}`` indicates when the
object was originally created as a current version.

Any return status in the 2nn range, such as 202 (Accepted), denotes
success. Status codes in the 4nn or 5nn range denote failure. If you
receive an error, you should retry your request. Note, however, that if
you specify a container that does not exist as your non-current version
container, a status of 412 (Precondition Failed) is returned when you
edit the versioned object. If you receive this error, verify that the
container exists.

When object versioning is enabled, requests on objects behave as
follows:

-  A **GET** request to a versioned object returns the current version
   of the object, with no request redirects or metadata lookups
   required.

-  A **POST** request to a versioned object updates only the current
   version of the object's metadata. It does not create a new version of
   the object. New versions are created when the content of the object
   changes.

-  A **DELETE** request to a versioned object removes the current
   version of the object and replaces it with the most recent
   non-current version, moving it from the non-current container to the
   current container. This most recent non-current version carries with
   it any metadata last set on it. If you want to completely remove an
   object and you have five total versions of it, you must perform five
   **DELETE** operations on it.

.. note:: A large-object manifest file cannot be versioned, but it can point to
   versioned segments.

To turn off object versioning on your current version container, remove
its ``X-Versions-Location`` metadata by sending a key value that is an
empty string.

**Example: Object versioning with cURL**

#. Create a version-storing container named ``versions``.

   .. code::

       curl -i -XPUT -H "X-Auth-Token: yourAuthToken" http://yourStorageUrl/versions

#. Create a container named ``current`` with a ``X-Versions-Location``
   header that references ``versions``.

   .. code::

       curl -i -XPUT -H "X-Auth-Token: yourAuthToken" \
       -H "X-Versions-Location: versions" http://yourStorageUrl/current

#. Create an object (the first version).

   .. code::

       curl -i -XPUT --data-binary 1 -H "X-Auth-Token: yourAuthToken" \
           http://yourStorageUrl/current/myobject

#. Create a new version of that object.

   .. code::

       curl -i -XPUT --data-binary 2 -H "X-Auth-Token: yourAuthToken" \
           http://yourStorageUrl}/current/myobject

#. See a list of the older versions of the object. (The example includes
   the hexadecimal number for the length of the file name.)

   .. code::

       curl -i -H "X-Auth-Token: yourAuthToken" \
           http://yourStorageUrl/versions?prefix=008myobject/

#. Delete the current version of the object and see that the older
   version is no longer in the ``versions`` container.

   .. code::

       curl -i -XDELETE -H "X-Auth-Token: yourAuthToken" \
           http://yourStorageUrl>/current/myobject
       curl -i -H "X-Auth-Token: yourAuthToken " \
           http://yourStorageUrl/versions?prefix=008myobject/
