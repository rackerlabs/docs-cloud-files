.. _gsg-gen-auth-token:

======================================
Generate an authentication token
======================================

This section includes information about the following topics:

-  Get your credentials 
-  Send the authentication request 
-  Receive the token 

To use the REST API, you must first obtain an authentication token. This
token will be passed in each Rackspace CDN API request in the
``X-Auth-Token`` header. You must generate a token whether you use cURL
or a REST client.

The example in this section demonstrates how to use cURL to obtain the
authentication token, as well as your account ID. You must supply both
when making subsequent Rackspace CDN API calls.


Get your credentials
~~~~~~~~~~~~~~~~~~~~

You must replace the names in the authenticate request examples in this
book with your values:

-  **yourUserName** — Your common Rackspace Cloud username, as supplied
   during registration

-  **yourApiKey** — Your API access key

   **To find your API key**

   1. Log in to the Cloud Control Panel (https://mycloud.rackspace.com).

   2. On the upper-right side of the top navigation pane, click your
      username.

   3. From the menu, select **Account Settings**.

   4. In the Login Details section of the Account Settings page, locate
      the **API Key** field and click **Show**.

   5. Copy the value of the API key and paste it into a text editor of
      your choice.

   6. Click **Hide** to hide the value of the API key.

You also need your cloud account ID. In the documentation, the account
ID is often referred to as your tenant name or tenant ID (technically,
the ID is different from the name, but at Rackspace, they are the same
thing). Together, three components—your username, your API key, and your
tenant ID or cloud account ID—form the authentication credentials that
are required to connect to the Rackspace cloud. To find your tenant ID
or cloud account ID, click your username on the upper-right side of the
top navigation pane in the Cloud Control Panel. The tenant ID or account
ID is listed first in the menu.

..  note:: 
    This guide uses **yourUserName** and **yourApiKey** for authentication.
    For information about other supported authentication methods, see
    the *Cloud Identity Client Developer Guide*.

Send the authentication request
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Use the following global endpoint to access the Cloud Identity Service:

-  ``https://identity.api.rackspacecloud.com/v2.0/``

You authenticate by using the URL
``https://identity.api.rackspacecloud.com/v2.0/tokens`` for the Cloud
Identity services, as shown in the following authentication request
example. Note that the ``v2.0`` component in the URL indicates that you
are using version 2.0 of the Cloud Identity API.

 
**Example: cURL authenticate request: JSON**

.. code::  

    curl -i -d \
    '{
        "auth":
        {
           "RAX-KSKEY:apiKeyCredentials":
           {
              "username": "yourUserName",
              "apiKey": "yourApiKey"}
        }
    }' \
    -H 'Content-Type: application/json' \
    'https://identity.api.rackspacecloud.com/v2.0/tokens'

This guide uses **yourUserName** and **yourApiKey** for authentication.
For information about other supported authentication methods, see the
in the Cloud Identity Client Developer Guide.



Receive the token
~~~~~~~~~~~~~~~~~


In the following example JSON authentication response, the ellipsis
(...) in the example represents other service endpoints, which are not
shown.

 
**Example: Authentication response: JSON**

.. code::  

    {
        "access": {
            "token": {
                "id": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
                "expires": "2014-11-24T22:05:39.115Z",           
                "tenant": {
                    "id": "110011",
                    "name": "110011"
                },
                "RAX-AUTH:authenticatedBy": [
                    "APIKEY"
                ]
             },
            "serviceCatalog": [
                {
                    "name": "cloudDatabases",
                    "endpoints": [
                        {
                            "publicURL": "https://syd.databases.api.rackspacecloud.com/v1.0/110011",
                            "region": "SYD",
                            "tenantId": "110011"
                        },
                        {
                            "publicURL": "https://dfw.databases.api.rackspacecloud.com/v1.0/110011",
                            "region": "DFW",
                            "tenantId": "110011"
                        },
                        {
                            "publicURL": "https://ord.databases.api.rackspacecloud.com/v1.0/110011",
                            "region": "ORD",
                            "tenantId": "110011"
                        },
                        {
                            "publicURL": "https://iad.databases.api.rackspacecloud.com/v1.0/110011",
                            "region": "IAD",
                            "tenantId": "110011"
                        },
                        {
                            "publicURL": "https://hkg.databases.api.rackspacecloud.com/v1.0/110011",
                            "region": "HKG",
                            "tenantId": "110011"
                        }
                    ],
                    "type": "rax:database"
                },
                
    ...        
                
                {
                    "name": "cloudDNS",
                    "endpoints": [
                        {
                            "publicURL": "https://dns.api.rackspacecloud.com/v1.0/110011",
                            "tenantId": "110011"
                        }
                    ],
                    "type": "rax:dns"
                },
                {
                    "name": "rackCDN",
                    "endpoints": [
                        {
                            "internalURL": "https://global.cdn.api.rackspacecloud.com/v1.0/110011",
                            "publicURL": "https://global.cdn.api.rackspacecloud.com/v1.0/110011",
                            "tenantId": "110011"
                        }
                    ],
                    
                    "type": "rax:cdn"
                }
            ],
            "user": {
                "id": "123456",           
                "roles": [
                    {
                        "description": "A Role that allows a user access to keystone Service methods",
                        "id": "6",
                        "name": "compute:default",
                        "tenantId": "110011"
                    },
                    {
                        "description": "User Admin Role.",
                        "id": "3",
                        "name": "identity:user-admin"
                    }
                ],
                "name": "jsmith",
                "RAX-AUTH:defaultRegion": "ORD"          
            }
        }
    }

The authentication token ``id`` is returned with an ``expires``
attribute that specifies when the token expires. Authentication tokens
are typically valid for 24 hours. Applications should be designed to
re-authenticate after receiving a 401 (Unauthorized) response from a
service endpoint.

..  note:: 
   For all response examples in this guide, the field values that you
   receive in your responses will vary from those shown here because
   they are specific to your account.

-  Remember to supply your authentication token wherever you see the
   field **yourAuthToken** in the examples in this guide.

-  The ``expires`` attribute denotes the time after which the token
   automatically becomes invalid. A token might be manually revoked
   before the time identified by the ``expires`` attribute; ``expires``
   predicts a token's maximum possible lifespan but does not guarantee
   that it will reach that lifespan. Clients are encouraged to cache a
   token until it expires.

The ``publicURL`` endpoints for ``raxcdn`` (for example
``https://global.cdn.api.rackspacecloud.com/v1.0/110011``) are also
returned in the response.

Your account ID number is located after the final backslash (/) in the
``publicURL`` field. In this example, you can see that the account ID is
110011. You need to specify your account ID on most of the Rackspace CDN
API calls, wherever you see the field **yourAccountID** specified in the
examples in this guide.

After authentication, you can use cURL to perform **GET**, **DELETE**,
**PATCH**, and **POST** requests for the Rackspace CDN API.
