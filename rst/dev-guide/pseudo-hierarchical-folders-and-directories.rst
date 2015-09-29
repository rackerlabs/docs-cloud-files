.. _pseudo-dir:

===========================================
Pseudo-hierarchical folders and directories
===========================================

Although you cannot nest directories in Cloud Files, you
can simulate a hierarchical structure within a single container by
adding forward slash characters (``/``) in the object name. To navigate
the pseudo-directory structure, you can use the ``delimiter`` query
parameter. This example shows you how to use pseudo-hierarchical folders
and directories.

.. note::

   In this example, the objects reside in a container called ``backups``.
   Within that container, the objects are organized in a pseudo-directory
   called ``photos``. The container name is not displayed in the example,
   but it is a part of the object URLs. For example, the URL of the
   picture ``me.jpg`` is
   ``https://storage.clouddrive.com/v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/backups/photos/me.jpg``.

To display a list of all the objects in the storage container, use
``GET`` without a ``delimiter`` or ``prefix``.

.. code::

    GET /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/backups

The system returns status code 200 (OK) and
the requested list of the objects.

.. code::

    photos/animals/cats/persian.jpg
    photos/animals/cats/siamese.jpg
    photos/animals/dogs/corgi.jpg
    photos/animals/dogs/poodle.jpg
    photos/animals/dogs/terrier.jpg
    photos/me.jpg
    photos/plants/fern.jpg
    photos/plants/rose.jpg

Use the delimiter parameter to limit the displayed results. To use
``delimiter`` with pseudo-directories, you must use the parameter slash
(``/``).

.. code::

    GET /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/backups?delimiter=/

The system returns status code 200 (OK) and
the requested matching objects. Because you use the slash, only the
pseudo-directory ``photos/`` displays. The returned values from a slash
``delimiter`` query are not real objects. They have a content-type of
``application/directory`` and are in the ``subdir`` section of JSON and
XML results.

.. code::

    photos/

Use the ``prefix`` and ``delimiter`` parameters to view the objects
inside a pseudo-directory, including further nested pseudo-directories.

.. code::

    GET /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/backups?prefix=photos/&delimiter=/

The system returns status code 200 (OK) and the objects and pseudo-directories within the top level pseudo-directory.

.. code::

    photos/animals/
    photos/me.jpg
    photos/plants/

You can create an unlimited number of nested pseudo-directories. To
navigate through them, use a longer ``prefix`` parameter coupled with
the ``delimiter`` parameter. In this sample output, there is a
pseudo-directory called ``dogs`` within the pseudo-directory
``animals``. To navigate directly to the files contained within
``dogs``, enter the following command:

.. code::

    GET /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/backups?prefix=photos/animals/dogs/&delimiter=/

The system returns status code 200 (OK) and
the objects and pseudo-directories within the nested pseudo-directory.

.. code::

    photos/animals/dogs/corgi.jpg
    photos/animals/dogs/poodle.jpg
    photos/animals/dogs/terrier.jpg