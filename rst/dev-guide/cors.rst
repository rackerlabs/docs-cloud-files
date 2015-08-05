====
CORS
====

..
   This is the section is a rewrite sent to David Goetz for review on
   9/3/2014 after Ken Perkins of the DRG sent email wanting the doc updated
   to include support for setting the access headers on object as noted in
   the OpenStack Object Storage reference for CORS. David Goetz hesitant to
   include all of this doc but it does reflect how things currently work.
   David is planning some dev changes so that container-level headers are
   the only way to do this - not object-level. But there is currently no
   ETA on the dev changes.

Cross-Origin Resource Sharing (CORS) is a mechanism that allows code
running in a browser to make requests to a domain other than the one
from which it originated by using HTTP headers, such as those assigned
by Cloud Files API requests.

Cloud Files supports CORS requests to containers and objects.

For more information about CORS and the access control headers, see
`www.w3.org/TR/access-control/ <http://www.w3.org/TR/access-control/>`__.

CORS headers for containers
~~~~~~~~~~~~~~~~~~~~~~~~~~~

..
  David Goetz provided the link for this information:
  https://github.com/openstack/swift/blob/master/doc/source/cors.rst. 

Container-level headers for CORS are used for the following Cloud Files
features:

-  :ref:`FormPost<cf-dg-formpost>` to enable your
   users to post to your site

-  :ref:`TempURL<cf-dg-tempurl>` to
   limit how long users can use a given URL


.. note::
   Container-level headers for CORS are not inherited for use with a
   CDN. For information about using object-level headers, which enable CORS to
   work over a CDN, see :ref:`CORS headers for objects<cf-dg-cors-objects>`.

CORS container headers enable your users to upload files from one
website, or origin, to your Cloud Files account. When you set the CORS
headers on your container, you provide Cloud Files with the following
information:

-  Which sites can post to your account

-  How often your container checks its allowed sites list

-  What headers to expose to the browser in the request response

CORS metadata is held on the container only. The values given apply to
the container itself and all objects within it.

The following table lists the container-level headers:

**Table: CORS container-level headers**

+------------------------------------+---------------------------------------+
| ``X-Container-Meta-Access-Control- | Specifies the origins that are        |
| Allow-Origin``                     | allowed to make cross-origin          |
|                                    | requests, separated by a space when   |
|                                    | there are multiple values.            |
+------------------------------------+---------------------------------------+
| ``X-Container-Meta-Access-Control- | Specifies the maximum age for the     |
| Max-Age``                          | origin to hold the preflight results, |
|                                    | in seconds (for example, 5, 10, or    |
|                                    | 1000).                                |
+------------------------------------+---------------------------------------+
| ``X-Container-Meta-Access-Control- | Specifies the headers that are        |
| Allow-Headers``                    | allowed in the actual request,        |
|                                    | separated by a space when there are   |
|                                    | multiple values.                      |
+------------------------------------+---------------------------------------+
| ``X-Container-Meta-Access-Control- | Indicates the headers exposed to the  |
| Expose-Headers``                   | browser in the actual request         |
|                                    | response, separated by a space when   |
|                                    | there are multiple values.            |
+------------------------------------+---------------------------------------+


To view the values for these headers, use the **HEAD** operation to show
container metadata. To delete the metadata, use the **DELETE** operation
to delete container metadata. (See `Cloud Files API v1 <http://api.rackspace.com/api-ref-files.html>`__ for operation descriptions.)


Before a browser issues an actual request, it might issue a preflight
request. The preflight request is an HTTP **OPTIONS** call to verify
that the origin is allowed to make the request. Following is the
sequence of actions:

#. The browser makes an **OPTIONS** request to Cloud Files.

#. Cloud Files returns either a 200 or 401 status code to the browser
   based on the allowed origins.

#. If Cloud Files returns 200, the browser makes the actual request
   (**DELETE**, **GET**, **HEAD**, **POST**, **PUT**) to Cloud Files.

When a browser receives a response to an actual request, it exposes only
those headers listed in the
``X-Container-Meta-Access-Control-Expose-Headers`` header. By default,
Cloud Files returns the following values for this header:

-  The simple response headers as listed at
   `www.w3.org/TR/cors/#simple-response-header/ <http://www.w3.org/TR/cors/#simple-response-header/>`__

-  The ``ETag``, ``X-Timestamp``, and ``X-Trans-Id`` headers

-  All metadata headers (``X-Container-Meta-*`` for containers and
   ``X-Object-Meta-*`` for objects)

-  Headers listed in ``X-Container-Meta-Access-Control-Expose-Headers``

To see some CORS JavaScript in action, follow these steps:

#. Copy and paste the text from Example: Test CORS
   page at the bottom of this section.

#. Host the page on a web server and note the protocol and hostname
   (origin) you will be using to request the page, for example
   ``http://localhost``.

#. Locate a container that you want to query. (The Cloud Files cluster
   hosting this container must have CORS support.)

#. Append the origin of the test page to the container’s
   ``X-Container-Meta-Access-Control-Allow-Origin`` header, using a
   request similar to the following example.

**Example of a CORS POST cURL request**

.. code::

    curl -X POST -H 'X-Auth-Token: yourAuthToken' \
      -H 'X-Container-Meta-Access-Control-Allow-Origin: http://localhost' \
       https://storage101.dfw1.clouddrive.com/v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer

At this point, the container is accessible to CORS clients hosted on
``http://localhost``. Open the test CORS page in your browser and
following these steps:

#. Populate the ``Token`` field.

#. Populate the ``URL`` field with the URL of either a container or
   object.

#. Select the request method.

#. Hit Submit.

If the request succeeds, the response header and body are displayed. If
the request did not succeed, the response status is 0.

**Example: Test CORS page**

.. code::

    <!DOCTYPE html>
    <html>
      <head>
        <meta charset="utf-8">
        <title>Test CORS</title>
      </head>
      <body>

        Token<br><input id="token" type="text" size="64"><br><br>

        Method<br>
        <select id="method">
            <option value="GET">GET</option>
            <option value="HEAD">HEAD</option>
            <option value="POST">POST</option>
            <option value="DELETE">DELETE</option>
            <option value="PUT">PUT</option>
        </select><br><br>

        URL (Container or Object)<br><input id="url" size="64" type="text"><br><br>

        <input id="submit" type="button" value="Submit" onclick="submit(); return false;">

        <pre id="response_headers"></pre>
        <p>
        <hr>
        <pre id="response_body"></pre>

        <script type="text/javascript">
          function submit() {
              var token = document.getElementById('token').value;
              var method = document.getElementById('method').value;
              var url = document.getElementById('url').value;

              document.getElementById('response_headers').textContent = null;
              document.getElementById('response_body').textContent = null;

              var request = new XMLHttpRequest();

              request.onreadystatechange = function (oEvent) {
                  if (request.readyState == 4) {
                      responseHeaders = 'Status: ' + request.status;
                      responseHeaders = responseHeaders + '\nStatus Text: ' + request.statusText;
                      responseHeaders = responseHeaders + '\n\n' + request.getAllResponseHeaders();
                      document.getElementById('response_headers').textContent = responseHeaders;
                      document.getElementById('response_body').textContent = request.responseText;
                  }
              }

              request.open(method, url);
              request.setRequestHeader('X-Auth-Token', token);
              request.send(null);
          }
        </script>

      </body>
    </html>

.. _cf-dg-cors-objects:

CORS headers for objects
~~~~~~~~~~~~~~~~~~~~~~~~

.. 
   *cyr - From "Assign CORS headers to requests" is in the OpenStack Object
   Storage Reference - headers for only objects. *

You can set object-level headers for CORS. Currently, using object-level
headers enables CORS to work over a CDN.

The following table lists the object-level headers:

**Table: CORS object-level headers**

+-----------------------+----------------------------------------------------+
| ``Access-Control-Allo | Specifies the origins that are allowed to make     |
| w-Origin``            | cross-origin requests, separated by a space when   |
|                       | there are multiple values.                         |
+-----------------------+----------------------------------------------------+
| ``Access-Control-Max- | Specifies the maximum age for the origin to hold   |
| Age``                 | the preflight results, in seconds (for example, 5, |
|                       | 10, or 1000).                                      |
+-----------------------+----------------------------------------------------+
| ``Access-Control-Expo | Specifies the headers exposed to the browser in    |
| se-Headers``          | the actual request response, separated by a space  |
|                       | when there are multiple values.                    |
+-----------------------+----------------------------------------------------+
| ``Access-Control-Allo | Indicates whether or not the response to the       |
| w-Credentials``       | request can be exposed when the credentials flag   |
|                       | is true.  When used as part of a response to a     |
|                       | preflight request, this indicates whether or not   |
|                       | the actual request can be made using credentials.  |
|                       | Note that simple GET requests are not preflighted, |
|                       | and so if a request is made for a resource with    |
|                       | credentials, if this header is not returned with   |
|                       | the resource, the response is ignored by the       |
|                       | browser and not returned to web content.           |
+-----------------------+----------------------------------------------------+
| ``Access-Control-Allo | Specifies the method or methods allowed when       |
| w-Methods``           | accessing the resource.  This is used in response  |
|                       | to a preflight request.                            |
+-----------------------+----------------------------------------------------+
| ``Access-Control-Requ | Used when issuing a preflight request to let the   |
| est-Headers``         | server know what HTTP headers will be used when    |
|                       | the actual request is made.                        |
+-----------------------+----------------------------------------------------+
| ``Access-Control-Requ | Used when issuing a preflight request to let the   |
| est-Method``          | server know what HTTP method will be used when the |
|                       | actual request is made.                            |
+-----------------------+----------------------------------------------------+
| ``Origin``            | Indicates the origin of the cross-site access      |
|                       | request or preflight request.                      |
+-----------------------+----------------------------------------------------+

The following example assigns the file origin to the ``Origin`` header
to indicate where the file came from. Doing so allows you to provide
security that requests to your Cloud Files repository are indeed from
the correct origination.

**Example: Assign CORS header request for an object**

.. code::

      PUT /apiVersion/yourAccountID/containerName/objectName HTTP/1.1
      Host: storage.clouddrive.com
      X-Auth-Token: yourAuthToken
      Origin: http://storage.clouddrive.com


