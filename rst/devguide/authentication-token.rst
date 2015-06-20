.. _cf-dg-auth:

==============
Authentication
==============

Every REST request against the Cloud Files service requires the
inclusion of a specific authorization token, supplied by the
``X-Auth-Token`` HTTP header. You obtain this token by using the
Rackspace Cloud Identity service and supplying a valid user name and API
access key.

Geographic endpoints
~~~~~~~~~~~~~~~~~~~~

The Rackspace Cloud Identity service serves as the entry point to all
Rackspace Cloud APIs and is itself a RESTful web service.

Use the following global endpoint to access the Rackspace Cloud Identity
service:

.. code::

    https://identity.api.rackspacecloud.com/v2.0/

Retrieving the authentication token
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+------------+---------------+--------------------------------------------------------+
| **POST**   | v2.0/tokens   | Authenticate to receive a token and a service catalog. |
+------------+---------------+--------------------------------------------------------+

Normal Status Code(s): 200, 203

Error Status Code(s): unauthorized (401), userDisabled (403), badRequest
(400), authFault (500), serviceUnavailable (503)

The authenticate operation provides clients with an authentication token
and a list of regional cloud endpoints.

.. note::
   For information about how to use cURL to retrieve the authentication token, see the *Cloud Files Getting Started Guide*.

The sample requests and responses in this section illustrate a general
case. In your authentication request, use your own credentials rather
than the sample values shown here for ``username`` and ``apiKey``. When
you authenticate successfully, the response to your authentication
request will include a catalog of the services to which you have
subscribed rather than the sample values shown here.

.. note::
   If you authenticate with ``username`` and ``password`` credentials, you can use multi-factor authentication to add an additional level of account security. This feature is not implemented for the ``username`` and ``apiKey`` credentials shown in the following examples.

For more information, see `Multi-factor authentication <http://docs.rackspace.com/auth/api/v2.0/auth-client-devguide/content/MFA_Ops.html>`_ in the *Cloud Identity Client Developer Guide*.

**Example: Authentication request: XML**

.. code::

    POST /v2.0/tokens HTTP/1.1
    User-Agent: curl/7.21.0 (x86_64-pc-linux-gnu) libcurl/7.21.0 OpenSSL/0.9.8o zlib/1.2.3.4 libidn/1.15 libssh2/1.2.6
    Host: identity.api.rackspacecloud.com
    Accept: application/xml
    Content-Type: application/xml
    Content-Length: 88

    <?xml version="1.0" encoding="UTF-8"?>
    <auth>   
       <apiKeyCredentials     
           xmlns="http://docs.rackspace.com/identity/api/ext/RAX-KSKEY/v1.0"     
           username="yourUserName"
           apiKey="yourApiKey"/>   
    </auth>


**Example: Authentication request: JSON**

.. code::

    POST /v2.0/tokens HTTP/1.1
    User-Agent: curl/7.21.0 (x86_64-pc-linux-gnu) libcurl/7.21.0 OpenSSL/0.9.8o zlib/1.2.3.4 libidn/1.15 libssh2/1.2.6
    Host: identity.api.rackspacecloud.com
    Accept: application/json
    Content-Type: application/json
    Content-Length: 54

    {
       "auth":
       {
          "RAX-KSKEY:apiKeyCredentials":
          {
             "username": "yourUserName",
             "apiKey": "yourApiKey"
          }
       }
    }

**Example: Authentication response: XML**

.. code::

    HTTP/1.1 200 OK
    Content-Type: application/xml; charset=UTF-8
    Content-Length: 477
    Date: Thu, 12 Apr 2012 18:50:20 GMT

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <access xmlns:os-ksadm="http://docs.openstack.org/identity/api/ext/OS-KSADM/v1.0"
      xmlns="http://docs.openstack.org/identity/api/v2.0"
      xmlns:rax-kskey="http://docs.rackspace.com/identity/api/ext/RAX-KSKEY/v1.0"
      xmlns:rax-ksqa="http://docs.rackspace.com/identity/api/ext/RAX-KSQA/v1.0"
      xmlns:common="http://docs.openstack.org/common/api/v1.0"
      xmlns:ksgrp="http://docs.rackspace.com/identity/api/ext/RAX-KSGRP/v1.0"
      xmlns:rax-kscatalog="http://docs.openstack.org/identity/api/ext/OS-KSCATALOG/v1.0"
      xmlns:atom="http://www.w3.org/2005/Atom">
      <token id="xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx" expires="2012-04-13T18:50:20.000-06:00"/>
      <user id="123456" name="yourUserName" rax-auth:defaultRegion="DFW">
        <roles>
          <role id="identity:admin" name="identity:admin" description="Admin Role."/>
          <role id="identity:default" name="identity:default" description="Default Role."/>
        </roles>
      </user>
      <serviceCatalog>
        <service type="rax:database" name="cloudDatabases">
          <endpoint region="DFW" tenantId="1100111" publicURL="https://dfw.databases.api.rackspacecloud.com/v1.0/1100111"/>
          <endpoint region="ORD" tenantId="1100111" publicURL="https://ord.databases.api.rackspacecloud.com/v1.0/1100111"/>
        </service>
        <service type="rax:load-balancer" name="cloudLoadBalancers">
          <endpoint region="DFW" tenantId="1100111" publicURL="https://dfw.loadbalancers.api.rackspacecloud.com/v1.0/1100111"/>
          <endpoint region="ORD" tenantId="1100111" publicURL="https://ord.loadbalancers.api.rackspacecloud.com/v1.0/1100111"/>
        </service>
        <service type="compute" name="cloudServersOpenStack">
          <endpoint region="DFW" tenantId="1100111"
            publicURL="https://dfw.servers.api.rackspacecloud.com/v2/1100111">
            <version id="2" info="https://dfw.servers.api.rackspacecloud.com/v2/"
              list="https://dfw.servers.api.rackspacecloud.com/" />
          </endpoint>
          <endpoint region="ORD" tenantId="1100111"
            publicURL="https://ord.servers.api.rackspacecloud.com/v2/1100111">
            <version id="2" info="https://ord.servers.api.rackspacecloud.com/v2/"
              list="https://ord.servers.api.rackspacecloud.com/" />
          </endpoint>
        </service>
        <service type="compute" name="cloudServers">
          <endpoint tenantId="1100111"
            publicURL="https://servers.api.rackspacecloud.com/v1.0/1100111">
            <version id="1.0"
              info="https://servers.api.rackspacecloud.com/v1.0/"
              list="https://servers.api.rackspacecloud.com/"/>
          </endpoint>
        </service>
        <service type="object-store" name="cloudFiles">
          <endpoint region="DFW"
            tenantId="MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"
            publicURL="https://storage101.dfw1.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"
            internalURL="https://snet-storage101.dfw1.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"/>
          <endpoint region="SYD"
            tenantId="MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"
            publicURL="https://storage101.syd2.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"
            internalURL="https://snet-storage101.syd2.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"/>
          <endpoint region="IAD"
            tenantId="MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"
            publicURL="https://storage101.iad3.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"
            internalURL="https://snet-storage101.iad3.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"/>
          <endpoint region="ORD"
            tenantId="MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"
            publicURL="https://storage101.ord1.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"
            internalURL="https://snet-storage101.ord1.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"/>
          <endpoint region="HKG"
            tenantId="MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"
            publicURL="https://storage101.hkg1.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"
            internalURL="https://snet-storage101.hkg1.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"/>
        </service>
        <service type="rax:object-cdn" name="cloudFilesCDN">
          <endpoint region="DFW"
            tenantId="MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"
            publicURL="https://cdn1.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"/>
          <endpoint region="SYD"
            tenantId="MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"
            publicURL="https://cdn4.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"/>
          <endpoint region="IAD"
            tenantId="MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"
            publicURL="https://cdn5.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"/>
          <endpoint region="HKG"
            tenantId="MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"
            publicURL="https://cdn6.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"/>
          <endpoint region="ORD"
            tenantId="MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"
            publicURL="https://cdn2.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"/>
        </service>
        <service type="rax:dns" name="cloudDNS">
          <endpoint tenantId="1100111"
            publicURL="https://dns.api.rackspacecloud.com/v1.0/1100111"/>
        </service>
      </serviceCatalog>
    </access>

**Example: Authentication response: JSON**

.. code::

    HTTP/1.1 200 OK
    Content-Type: application/json; charset=UTF-8
    Content-Length: 477
    Date: Thu, 12 Apr 2012 18:45:13 GMT

    {
        "access": {
         
            "token": {
                "expires": "2012-04-13T18:45:13.000-06:00",
                "id": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
            }, 
            "user": {
                "id": "123456", 
                "name": "userUserName",
                "RAX-AUTH:defaultRegion": "DFW",
                "roles": [
                    {
                        "description": "Admin Role.", 
                        "id": "identity:admin", 
                        "name": "identity:admin"
                    }, 
                    {
                        "description": "Default Role.", 
                        "id": "identity:default", 
                        "name": "identity:default"
                    }
                ]
            },
            "serviceCatalog": [
                {
                    "endpoints": [
                        {
                            "publicURL": "https://dfw.databases.api.rackspacecloud.com/v1.0/1100111", 
                            "region": "DFW", 
                            "tenantId": "1100111"
                        }, 
                        {
                            "publicURL": "https://ord.databases.api.rackspacecloud.com/v1.0/1100111", 
                            "region": "ORD", 
                            "tenantId": "1100111"
                        }
                    ], 
                    "name": "cloudDatabases", 
                    "type": "rax:database"
                },
                {
                    "endpoints": [
                        {
                            "publicURL": "https://dfw.loadbalancers.api.rackspacecloud.com/v1.0/1100111", 
                            "region": "DFW", 
                            "tenantId": "1100111"
                        }, 
                        {
                            "publicURL": "https://ord.loadbalancers.api.rackspacecloud.com/v1.0/1100111", 
                            "region": "ORD", 
                            "tenantId": "1100111"
                        }
                    ], 
                    "name": "cloudLoadBalancers", 
                    "type": "rax:load-balancer"
                }, 
                {
                    "endpoints": [
                        {
                            "tenantId": "1100111",
                            "region": "DFW",
                            "publicURL": "https://dfw.servers.api.rackspacecloud.com/v2/1100111", 
                            "versionId": "2", 
                            "versionInfo": "https://dfw.servers.api.rackspacecloud.com/v2/", 
                            "versionList": "https://dfw.servers.api.rackspacecloud.com/"
                        },
                        {
                            "tenantId": "1100111",
                            "region": "ORD",
                            "publicURL": "https://ord.servers.api.rackspacecloud.com/v2/1100111", 
                            "versionId": "2", 
                            "versionInfo": "https://ord.servers.api.rackspacecloud.com/v2/", 
                            "versionList": "https://ord.servers.api.rackspacecloud.com/"
                        }
                    ],
                    "name": "cloudServersOpenStack", 
                    "type": "compute"
                },
                {
                    "endpoints": [
                        {
                            "tenantId": "1100111", 
                            "publicURL": "https://servers.api.rackspacecloud.com/v1.0/1100111", 
                            "versionId": "1.0", 
                            "versionInfo": "https://servers.api.rackspacecloud.com/v1.0/", 
                            "versionList": "https://servers.api.rackspacecloud.com/"
                        }
                    ],
                    "name": "cloudServers", 
                    "type": "compute"
                },
                {
                    "endpoints": [
                        {
                            "publicURL": "https://cdn1.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee",
                            "region": "DFW",
                            "tenantId": "MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"
                        },
                        {
                            "publicURL": "https://cdn4.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee",
                            "region": "SYD",
                            "tenantId": "MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"
                        },
                        {
                            "publicURL": "https://cdn5.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee",
                            "region": "IAD",
                            "tenantId": "MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"
                        },
                        {
                            "publicURL": "https://cdn6.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee",
                            "region": "HKG",
                            "tenantId": "MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"
                        },
                        {
                            "publicURL": "https://cdn2.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee",
                            "region": "ORD",
                            "tenantId": "MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"
                        }
                    ],
                    "name": "cloudFilesCDN",
                    "type": "rax:object-cdn"
              },
              {
                    "endpoints": [
                        {
                            "internalURL": "https://snet-storage101.dfw1.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee",
                            "publicURL": "https://storage101.dfw1.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee",
                            "region": "DFW",
                            "tenantId": "MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"
                        },
                        {
                            "internalURL": "https://snet-storage101.syd2.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee",
                            "publicURL": "https://storage101.syd2.clouddrive.com/v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880321",
                            "region": "SYD",
                            "tenantId": "MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"
                        },
                        {
                            "internalURL": "https://snet-storage101.iad3.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee",
                            "publicURL": "https://storage101.iad3.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee",
                            "region": "IAD",
                            "tenantId": "MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"
                        },
                        {
                            "internalURL": "https://snet-storage101.ord1.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee",
                            "publicURL": "https://storage101.ord1.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee",
                            "region": "ORD",
                            "tenantId": "MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"
                        },
                        {
                            "internalURL": "https://snet-storage101.hkg1.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee",
                            "publicURL": "https://storage101.hkg1.clouddrive.com/v1/MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee",
                            "region": "HKG",
                            "tenantId": "MossoCloudFS_aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"
                        }
                    ],
                    "name": "cloudFiles",
                    "type": "object-store"
                },
                {
                    "endpoints": [
                        {
                            "tenantId": "1100111",
                            "publicURL": "https://dns.api.rackspacecloud.com/v1.0/1100111"
                        }
                    ],
                    "name": "cloudDNS", 
                    "type": "rax:dns"
                }
            ]
        }
    }

Cloud Files service endpoints are published in the service catalog in
the authentication response with the account information, which is a
required element of the service endpoints. The examples shown in this
document are for authentication for US customers. Customers with
UK-based accounts see different values in the service catalog. For more
information about service endpoints, see the section called “Service
access endpoints”.

