===================================
Enabling bypass of browser behavior
===================================

When an object is assigned the ``Content-Disposition`` header, you can
override a browser's default behavior for a file so that the browser
prompts to save the file rather than displaying it by using default
browser settings.

In the following example, the ``Content-Disposition`` header is assigned
with an attachment type that indicates how the file should be
downloaded.

**Example: Content-Disposition: HTTP request**

.. code::

    PUT /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer/MyObject HTTP/1.1
    Host: storage.clouddrive.com
    X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c
    Content-Type: image/tiff
    Content-Disposition: attachment; filename=platmap.tif
