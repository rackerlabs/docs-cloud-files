===================
Access log delivery
===================

You can use access log delivery to analyze the number of requests for
each object, the client IP address, and time-based usage patterns (such
as monthly or seasonal usage).

Access log delivery is set on the container, and every object in the
container is tracked. To enable access logs for a container, set the
metadata ``X-Container-Meta-Access-Log-Delivery`` header to ``True``. If
you have multiple containers that you want to track, you must set the
metadata header to ``TRUE`` for each container. When your first log is
delivered, the container .ACCESS\_LOGS is created. This container holds
the access logs for every container for which you turn on logging. Log
files exist until you delete them. To turn off logging, set the
``X-Container-Meta-Access-Log-Delivery`` header to ``FALSE``.

Log files are named according to the following pattern: container name,
log date, log hour, and MD5 hash. For example::

      ``Media/2012/10/01/16/096e6c4473f235db081deb51f42a8d98.log.gz``

In this example, ``Media`` is the name of the container, 2012/10/01 is
the date (October 1, 2012), and 16 is the hour that the log file was
created. There might be multiple files for a given hour because the
storage system splits log files based on both time and log file size.
All times in the access logs are UTC time.

Within the gzip logs, the format of the entries is similar to National
Center for Supercomputing Applications (NCSA) combined log format, but
without cookies. The pattern follows. The dashes (*``-``*) denote fields
that the NCSA combined log format dictates be present but that Cloud
Files does not capture.

``client_ip - - [day/month/year:hour:minute:second timezone] “method request HTTP_version” return_code bytes_sent “referrer” “user_agent”``

The following example shows log entries.

**Example: Access log entries**

.. code::

       50.56.228.64 - - [27/08/2012:16:50:22 +0000] "PUT /v1/
            MossoCloudFS_bb88c7b9-ea5b-49af-82fc-376ff241963c/CharacterTest_%2521 
            HTTP/1.0" 401 0 "-" "python-requests/0.13.8 
            CPython/2.7.3 Linux/3.2.0-29-generic"
       50.56.228.64 - - [27/08/2012:16:53:49 +0000] "PUT /v1/
            MossoCloudFS_bb88c7b9-ea5b-49af-82fc-376ff241963c/CharacterTest_%2521
            /object_%2521 HTTP/1.0" 201 118 "-" "python-requests/0.13.8 
            CPython/2.7.3 Linux/3.2.0-29-generic"  
       50.56.228.64 - - [27/08/2012:16:53:47 +0000] "PUT /v1/
            MossoCloudFS_bb88c7b9-ea5b-49af-82fc-376ff241963c/CharacterTest_%2521 
            HTTP/1.0" 202 58 "-" "python-requests/0.13.8 
            CPython/2.7.3 Linux/3.2.0-29-generic"       
       50.56.228.64 - - [27/08/2012:16:50:36 +0000] "PUT /v1/
            MossoCloudFS_bb88c7b9-ea5b-49af-82fc-376ff241963c/CharacterTest_%2521 
            HTTP/1.0" 401 0 "-" "python-requests/0.13.8 
            CPython/2.7.3 Linux/3.2.0-29-generic"
