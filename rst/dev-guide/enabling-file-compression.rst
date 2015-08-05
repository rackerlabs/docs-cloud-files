=========================
Enabling file compression
=========================

The ``Content-Encoding`` header allows a file to be compressed while
still preserving the identity of the underlying media type of the file,
for example, a video.

The object must be compressed before it is uploaded. Cloud Files does
not perform any automatic compression. The ``Content-Encoding`` header
enables the client to set the metadata appropriately.

.. note::
   The Rackspace CDN provider, Akamai, encodes HTML, JavaScript, and CSS
   files in gzip format. However, in your Cloud Files account, your files
   are not encoded. For more information, see the blog post `Cloud Files
   CDN Compresses at the
   Edge <http://www.rackspace.com/blog/cloud-files-cdn-compresses-at-the-edge/>`__.
   Compressing these objects helps lower costs and increases download
   speeds.

In the following example, the ``Content-Encoding`` header indicates the
type of encoding used on the data.

**Example: Content-Encoding: HTTP request**

.. code::

    PUT /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer HTTP/1.1
    Host: storage.clouddrive.com
    X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c
    Content-Type: video/mp4
    Content-Encoding: gzip
