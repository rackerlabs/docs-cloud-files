.. _set-error-pages-for-a-static-website:

Set error pages for a static website
------------------------------------

Error pages are served with the status code prepended to the name of the
error page that you set. For example, if you set
``X-Container-Meta-Web-Error`` to ``error.html``, 401 errors display the
page ``401error.html``. Similarly, 404 errors display ``404error.html``.
You must have both of these pages created in your container when you set
the ``X-Container-Meta-Web-Error`` metadata, or your site will display
generic error pages.

Set the ``X-Container-Meta-Web-Error`` metadata once for your entire
static website.

**Example: Set error pages for static website: HTTP request**

.. code::

    POST /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer HTTP/1.1
    Host: storage.clouddrive.com
    X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c
    X-Container-Meta-Web-Error: error.html            

Any class 200 status code indicates success.

