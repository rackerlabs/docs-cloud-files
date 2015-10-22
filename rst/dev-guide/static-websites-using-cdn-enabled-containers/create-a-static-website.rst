.. _create-a-static-website:


Create a static website
-----------------------

You can use your Cloud Files account to create a static website. First,
you must CDN-enable a storage container. Any HTML or static web pages in
the container become available through a static website after you set
the ``X-Container-Meta-Web-Index`` header to ``index.html`` or another
index page of your choice. You can also create subdirectories in your
website by creating pseudo directories, as outlined in :ref:`Pseudo hierarchical directories and folders<pseudo-dir>`. Each
pseudo directory becomes a subdirectory in the website.

The page you set for ``X-Container-Meta-Web-Index`` becomes the index
page for every subdirectory in your website. Each of your pseudo
directories must contain a file with that name. So, if you set
``X-Container-Meta-Web-Index`` to ``index.html``, you must have an
``index.html`` page in each pseudo directory. For example, suppose that
you have a ``subdir`` pseudo directory. If you do not have an
``index.html`` page in ``subdir``, visits to ``myhost/subdir/`` return a
status code 404 (Not Found).

You also have the option of displaying a list of HTML files in your
pseudo directory, instead of a web page. You do this by setting the
``X-Container-Meta-Web-Listings`` header to ``True``. If listings are
enabled, you can add styles to your file list by setting
``X-Container-Meta-Web-Listings-CSS`` to a style sheet. For example,
setting ``X-Container-Meta-Web-Listings-CSS: listing.css`` makes
listings link to the ``listing.css`` style sheet. To view the HTML
elements to which you can add styles, use your browser to view the HTML
source on the listing page.

You can modify the ``Content-Type`` of directory marker objects by
setting the ``X-Container-Meta-Web-Directory-Type`` header. If this
header is not set, ``application/directory`` is used by default.
Directory marker objects are 0-byte objects that represent directories
to create a simulated hierarchical structure.

The following instructions describe using a CNAME with your DNS Server (or
name server). The CNAME is the domain name of your site (such as
www.rackspace.com). Your CNAME is set up with your individual DNS
Server. For more information about using CNAMEs, see the *Cloud DNS
Developer Guide*.
After your CNAME is established, set the CNAME to your Cloud Files CDN
URI to get your site up and running on the web.

**Set up a static website**

Following are the step-by-step instructions for setting up a static
website.

#. Create a container.

#. Upload your pages to the container.

#. Set the index (or primary page) for your website by performing a
   **POST** request to the header ``X-Container-Meta-Web-Index`` on your
   website's container. See the following example. (Remember to change the
   ``X-Auth-Token`` to your authentication token.) You must use your
   storage URL and the container name to properly point to the container
   (``storageURL``/``containerName``).

   (You get your authentication token when you authenticate your session
   as shown in :ref:`Authentication<auth>`.)

#. CDN-enable your container. (See in the operation :ref:`CDN-enable and CDN-disable a container <put-cdn-enable-and-cdn-disable-a-container>`.)

#. Go to your domain host and set up a CNAME using your CDN URI
   (``X-Cdn-Uri``). The CNAME is the domain or branded URI that you use
   instead of the CDN URI. If you need to find your CDN URI, perform a
   **HEAD** request to ``cdn.clouddrive.com`` as shown in the
   description of the operation to list metadata for a CDN-enabled
   container.

#. To view your website online, visit your CDN URI or your CNAME domain.

**Example: Set up static web**

.. code::

    cURL -X POST -H "X-Container-Meta-Web-Index: index.html" -H "X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c" "https://storage101.dfw1.clouddrive.com/v1/MossoCloudFS_a55df/MyLibrary/"

After your container has an index page set and your domain host has your
CNAME recorded, your static website is ready.

**Example: Container setup for static website**

.. code::

    container/index.html
    container/page2.html
    container/subdir/index.html
    container/subdir/pageX.html

In the following results, the CNAME is ``myhost``, and the
``X-Container-Meta-Web-Index`` is set to ``index.html``. The results on
the right of the example are the pages that display in the web browser.

**Example: Static website enabled container results**

.. code::

    http://myhost                     Displays container/index.html
    http://myhost/page2.html          Displays container/page2.html
    http://myhost/subdir              Displays container/subdir/index.html
    http://myhost/subdir/             Displays container/subdir/index.html
    http://myhost/subdir/pageX.html   Displays container/subdir/pageX.html

.. note::
   To disable a static website that you have created, send a request to
   remove the metadata header that created the static web site (for
   example, ``X-Container-Meta-Web-Index``).

