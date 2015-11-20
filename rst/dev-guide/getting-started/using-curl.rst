.. _gsg-using-curl:

Sending API requests by using cURL
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

cURL is a command-line tool that you can use to interact with REST
interfaces. cURL lets you transmit and receive HTTP requests and
responses from the command line or a shell script, which enables you to
work with the API directly (without using one of the language-specific
APIs). cURL is available for most UNIX system-based environments, Apple
Mac OS X®, and Microsoft Windows®. For more information about cURL, see
http://curl.haxx.se/.

The following cURL command-line options are used in this guide to run
the examples.

**Table: cURL command-line options**

+--------------------+--------------------------------------------------------+
| Option             | Description                                            |
+====================+========================================================+
| ``-d``             | Sends the specified data in a **POST** request to the  |
|                    | HTTP server.                                           |
+--------------------+--------------------------------------------------------+
| ``-i``             | Includes the HTTP header in the output.                |
+--------------------+--------------------------------------------------------+
| ``-H HEADER``      | Specifies an HTTP header in the request. You can       |
|                    | specify any number of extra headers. Precede each      |
|                    | header with the -H option.                             |
+--------------------+--------------------------------------------------------+
| ``-s``             | Specifies silent or quiet mode. Does not show progress |
|                    | or error messages. If your cURL command is not         |
|                    | generating any output, try replacing the ``-s`` option |
|                    | with ``-i``.                                           |
+--------------------+--------------------------------------------------------+
| ``-X``             | Specifies the request operation to use when            |
|                    | communicating with the HTTP server. The specified      |
|                    | request is used instead of the default operation,      |
|                    | which is **GET**. For example, ``-X PUT`` specifies to |
|                    | use the **PUT** operation.                             |
+--------------------+--------------------------------------------------------+



..  note:: 
    If you have the tools, you can run the cURL JSON request examples with
    the following option to format the output from cURL: **<cURL JSON
    request example> \| python -m json.tool**.
