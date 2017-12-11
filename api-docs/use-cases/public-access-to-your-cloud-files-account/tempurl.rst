.. _tempurl:

TempURL
~~~~~~~

You can use the Temporary URL feature (TempURL) to create limited-time
Internet addresses that allow limited access to your Cloud Files
account. Using TempURL, you can allow others to retrieve objects from or
place objects in your Cloud Files account for a specified amount of
time. After the specified amount of time expires, access to the account
with the TempURL is denied.

.. note::
   If the access time expires while a large file is being retrieved, the
   download continues until it is finished. Only the link expires.

Access to your Cloud Files account or website with a TempURL is
independent of whether your account is CDN-enabled. Even if you do not
CDN-enable a directory, you can still grant temporary public access
through a TempURL. When you create a TempURL, Cloud Files validates a
**GET**-accessible or **PUT**-accessible URL, which is time-limited.

.. note::
   The TempURL is the same thing as the TempURL Secret, and is set using
   the TempURL metadata key described in the next section. The TempURL is
   the actual URL.

Set account TempURL metadata key
--------------------------------

To create a TempURL, you must first set the
``X-Account-Meta-Temp-Url-Key`` metadata header on your Cloud Files
account to a key that only you know. This key can be any arbitrary
sequence.

.. note::
   Changing the ``X-Account-Meta-Temp-URL-Key`` invalidates any
   previously generated TempURLs within 60 seconds (the cache time for the
   key). To allow transitioning to a new key without effecting service, Cloud
   Files supports up to two keys, specified by ``X-Account-Meta-Temp-URL-Key``
   and ``X-Account-Meta-Temp-URL-Key-2``. Signatures are checked against
   both keys, if present. Testing both keys enables key rotation without
   invalidating all existing TempURLs — you can create TempURLs with a new
   key while allowing TempURLs created with the original key to remain
   valid. Once all the TempURLs generated with the old key have been
   exhausted, you can change or remove the old key.

**Example: Set account metadata key for public access: HTTP
request**

.. code::

    POST /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123 HTTP/1.1
    Host: storage.clouddrive.com
    X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c
    X-Account-Meta-Temp-Url-Key: yourKey

Any class 200 status code indicates success.

Create the TempURL
------------------

After the metadata is set, you must create an HMAC-SHA256 (RFC 2403)
signature. When you generate the TempURL, you determine which method of
access you will grant users, **GET** or **PUT**. You also determine the
path to the object to which you are granting access. Lastly, you set the
time for your TempURL to expire in UNIX epoch notation.

.. note::

   You can also use HMAC-SHA1 (RFC 2104) with TempURL, but HMAC-SHA256 is
   stronger cyrtographically.

In the following examples, a TempURL that will be available for 60
seconds is generated for the my\_cat.jpg object. The ``key`` in the
examples is the value of ``X-Account-Meta-Temp-Url-Key``.

**Example: Create TempURL (in Python)**

.. code::

      import hmac
      from hashlib import sha256
      from sys import argv
      from time import time

      if len(argv) != 5:
        print 'Syntax: <method> <url> <seconds> <key>'
        print 'Example: GET https://storage101.dfw1.clouddrive.com/v1/' \
            'MossoCloudFS_12345678-9abc-def0-1234-56789abcdef0/' \
            'container/my_cat.jpg 60 my_shared_secret_key'
      else:
        method, url, seconds, key = argv[1:]
        method = method.upper()
        base_url, object_path = url.split('/v1/')
        object_path = '/v1/' + object_path
        seconds = int(seconds)
        expires = int(time() + seconds)
        hmac_body = '%s\n%s\n%s' % (method, expires, object_path)
        sig = hmac.new(key, hmac_body, sha256).hexdigest()
        print '%s%s?temp_url_sig=%s;temp_url_expires=%s' % \
            (base_url, object_path, sig, expires)

Be certain to use the full URL to the object, just as you would with a
normal request.

In this example, the signature might be
da39a3ee5e6b4b0d3255bfef95601890afd80709 and the expire time might
translate to 1323479485 because the signature and expire time completely
depend on the time when the code runs. On your website, you would
provide a link to the following URL:

.. code::

      https://storage.clouddrive.com/v1/AUTH_account/container/my_cat.jpg?
      temp_url_sig=da39a3ee5e6b4b0d3255bfef95601890afd80709&
      temp_url_expires=1323479485

If you do not provide users with the exact TempURL, they get a 401
(Unauthorized) status code. **HEAD** queries are allowed if **GET** or
**PUT** operations are allowed.

**Example: Create TempURL (in PHP)**

.. code::

      <?php
      if ($argc != 5) {
          echo "Syntax: <method> <url> <seconds> <key>";
          echo "Example: GET https://storage101.dfw1.clouddrive.com/v1/" .
               "MossoCloudFS_12345678-9abc-def0-1234-56789abcdef0/" .
               "container/my_cat.jpg 60 my_shared_secret_key";
      } else {
        $method = $argv[1];
        $url = $argv[2];
        $seconds = $argv[3];
        $key = $argv[4];
        $method = strtoupper($method);
        list($base_url, $object_path) =  split("/v1/", $url);
        $object_path = "/v1/$object_path";
        $seconds = (int)$seconds;
        $expires = (int)(time() + $seconds);
        $hmac_body = "$method\n$expires\n$object_path";
        $sig = hash_hmac("sha256", $hmac_body, $key);
        echo "$base_url$object_path?" .
             "temp_url_sig=$sig&temp_url_expires=$expires";
      }
      ?>

**Example: Create TempURL (in Ruby)**

.. code::

      require "openssl"

      unless ARGV.length == 4
          puts "Syntax: <method> <url> <seconds> <key>"
          puts ("Example: GET https://storage101.dfw1.clouddrive.com/v1/" +
              "MossoCloudFS_12345678-9abc-def0-1234-56789abcdef0/" +
              "container/path/to/object.file 60 my_shared_secret_key")
      else
          method, url, seconds, key = ARGV
          method = method.upcase
          base_url, object_path = url.split(/\/v1\//)
          object_path = '/v1/' + object_path
          seconds = seconds.to_i
          expires = (Time.now + seconds).to_i
          hmac_body = "#{method}\n#{expires}\n#{object_path}"
          sig = OpenSSL::HMAC.hexdigest("sha256", key, hmac_body)
          puts ("#{base_url}#{object_path}?" +
              "temp_url_sig=#{sig}&temp_url_expires=#{expires}")
      end

.. _override-tempurl-fn:

Override TempURL file names
---------------------------

TempURLs support the ``filename`` query parameter, which you can use to
override the ``Content-Disposition`` header and indicate to the browser
a file name in which to save the file. In the following example, you see
the usual TempURL without the file name override.

**Example: TempURL without file name override**

.. code::

    https://cf-cluster.example.com/v1/AUTH_account/container/object?
    temp_url_sig=da39a3ee5e6b4b0d3255bfef95601890afd80709&
    temp_url_expires=1323479485


In the following example, you see ``&filename=bob.txt`` appended to the
TempURL to indicate to the browser to save the file as ``bob.txt``:

**Example: TempURL with file name override - Example 1**

.. code::

    https://cf-cluster.example.com/v1/AUTH_account/container/object?
    temp_url_sig=da39a3ee5e6b4b0d3255bfef95601890afd80709&
    temp_url_expires=1323479485&
    filename=bob.txt

With GET TempURLs, a ``Content-Disposition`` header is set on the
response so that browsers interpret this as a file attachment to be
saved. The file name chosen is based on the object name, but you can
override this with a ``filename`` query parameter. The following example
specifies a filename of ``My Test File.pdf``:

**Example: TempURL with file name override - Example 2**

.. code::

    https://cf-cluster.example.com/v1/AUTH_account/container/object?
    temp_url_sig=da39a3ee5e6b4b0d3255bfef95601890afd80709&
    temp_url_expires=1323479485&
    filename=My+Test+File.pdf

If you do not want the object to be downloaded, you can cause
``Content-Disposition: inline`` to be set on the response by adding the
``inline`` parameter to the query string:

**Example: TempURL with inline query parameter**

.. code::

    https://cf-cluster.example.com/v1/AUTH_account/container/object?
    temp_url_sig=da39a3ee5e6b4b0d3255bfef95601890afd80709&
    temp_url_expires=1323479485&
    inline
