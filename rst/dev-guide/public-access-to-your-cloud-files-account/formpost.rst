.. _cf-dg-formpost:


========
FormPost
========

You can use the FormPost feature to give your website audience a way to
upload objects to your Cloud Files account through a web form. FormPost
works by translating a browser form request into an object **PUT**
operation in Cloud Files. After you enable FormPost on your account, you need
only to create the form in your website by using the guidelines in this
section.

As with all objects in Cloud Files, the object file size limit is 5 GB.
If your users try to upload an object larger than 5 GB, they will get a
file size error.

Set account metadata key
~~~~~~~~~~~~~~~~~~~~~~~~

To allow FormPost actions on your Cloud Files account, you must first
set the ``X-Account-Meta-Temp-Url-Key`` metadata header on your Cloud
Files account to a key that only you know. This key can be any arbitrary
sequence.

After you set the key, do not change it while you still want others to
access your account. If you change it, the actions from a FormPost
become invalid (within 60 seconds, which is the cache time for a key).

.. note::
   The **POST** URI should not include the final container. Include just
   the version and your account, like
   ``/v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123`` shown in the
   example below. If you include the full path to the container, the key is
   not set properly.

**Example: Set account metadata key for public access: HTTP request**

.. code::

    POST /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123 HTTP/1.1
    Host: storage.clouddrive.com
    X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c
    X-Account-Meta-Temp-Url-Key: yourKey

Any class 200 status code indicates success.

Create the form
~~~~~~~~~~~~~~~

To communicate between your website and your Cloud Files account, create
a form using the following format in your website:

**Example: Layout of web form**

.. code::

      <form action="<CF-url>" method="POST" enctype="multipart/form-data">
        <input type="hidden" name="redirect" value="<redirect-url>" />
        <input type="hidden" name="max_file_size" value="<bytes>" />
        <input type="hidden" name="max_file_count" value="<count>" />
        <input type="hidden" name="expires" value="<unix-timestamp>" />
        <input type="hidden" name="signature" value="<hmac>" />
        <input type="hidden" name="x_delete_at" value="<unix-timestamp>" />
        <input type="hidden" name="x_delete_after" value="<seconds>" />
        <input type="file" name="file1" /><br />
        <input type="submit" />
      </form>

The parameters and attributes in the form are defined as follows:

-  *(Required)* The ``form action`` attribute is the Cloud Files URL
   (``CF-url``) to the destination where files will be uploaded. For
   example,
   ``https://storage.clouddrive.com/v1/yourAccountID/container``. The
   name of each uploaded object has the ``<CF-url>`` appended to the
   front of it.

   .. note:: Optionally, you can also include a prefix to separate uploads, such as assigning each user a certain prefix:

        https://storage.clouddrive.com/v1/yourAccountID/container/object_prefix.

-  *(Required)* The ``method`` attribute must be ``POST`` and the
   ``enctype`` must be set as ``multipart/form-data``.

-  *(Optional)* The ``redirect`` attribute is the URL of the page that
   is displayed on your website after the form processes. The URL will
   have status and message query parameters added to it, indicating the
   HTTP status code for the upload (2nn indicates success) and a
   possible message for more information if there is an error, such as
   ``max_file_size exceeded``.

   .. note::
        Although the ``redirect`` attribute is optional for the form, it must be present in the HMAC body (shown in the following example). Although ``redirect`` must be present, its value can be an empty string to indicate that no ``redirect`` is included on the form.

-  *(Required)* The ``max_file_size`` attribute specifies the maximum
   size in bytes of the largest single file upload. Because the storage
   system maximum file size is 5 GB, ``max_file_size`` cannot exceed 5
   GB.

-  *(Required)* The ``max_file_count`` attribute specifies the maximum
   number of files that can be uploaded with the form. If you send more
   files than specified by ``max_file_count``, Cloud Files uploads the
   files as normal until you hit the limit (the ``max_file_count``
   value). Then, Cloud Files sends an error when it is trying to create
   the file over the ``max_file_count`` value.

   .. note::
        The ``max_file_count`` value used to generate the ``signature`` must be the same as that in the web form.

-  *(Required)* The ``expires`` attribute is the UNIX timestamp when the
   form is invalidated. This gives your website users a limited time to
   have the form open. Time must be in UNIX epoch format.

   .. note::
        The ``expires`` in the web form and ``expires`` in the HMAC must be the same.

-  *(Required)* The ``signature`` attribute is the HMAC-SHA1 signature
   of the form. Following is sample code for computing the signature in
   Python:

   **Example: Generate signature for FormPost**

   .. code::

         import hmac
         from hashlib import sha1
         from time import time
         path = '/v1/account/container/object_prefix'
         redirect = 'https://myserver.com/some-page'  # set to '' if redirect not in form 
         max_file_size = 104857600
         max_file_count = 10
         expires = int(time() + 600)
         key = 'mykey'
         hmac_body = '%s\n%s\n%s\n%s\n%s' % (path, redirect,
             max_file_size, max_file_count, expires)
         signature = hmac.new(key, hmac_body, sha1).hexdigest()

   Be sure to use the full path in your Cloud Files account, from the
   ``/v1/`` onward.

   Note that ``x_delete_at`` and ``x_delete_after`` (see below) are not
   used in signature generation because they are optional attributes.

   The ``key`` value is the value of the ``X-Account-Meta-Temp-Url-Key``
   header set for the account.

   .. note::
        If you receive the ``Invalid Signature`` error, use the **HEAD** operation to confirm that your key matches the value in the response from the **HEAD** command.

-  *(Optional)* If you want the uploaded files to be temporary, you can
   set the ``x-delete-at`` or ``x-delete-after`` attributes by adding
   one of these as a form input.

-  *(Required)* The ``type="file"`` attribute defines the form file
   field. You must have at least one entry to allow your users to select
   and upload a file, but you can add more fields for multiple files.
   However, the number of entries must not exceed the value of
   ``max_file_count``. Each ``type="file"`` attribute must have a
   different name.

   .. note::
        The ``type="file"`` attribute or attributes must be at the end of the form code for Cloud Files to process the uploads correctly.

