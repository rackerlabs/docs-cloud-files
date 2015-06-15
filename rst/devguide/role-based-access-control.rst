=========================
Role Based Access Control
=========================

Role Based Access Control (RBAC) restricts access to the capabilities of
Rackspace Cloud services, including the Cloud Files API, to authorized
users only. RBAC enables Rackspace Cloud customers to specify which
account users of their Cloud account have access to which Cloud Files
API service capabilities, based on roles defined by Rackspace (see
`Table 1.1, “Cloud Files product roles and
permissions” fixmefixmefixme#RBAC_product_roles_table>`__). The
permissions to perform certain operations in the Cloud Files API –
create, read, update, delete – are assigned to specific roles, and the
Cloud account admin user assigns these roles to account users.

Assigning roles to account users
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The account owner (identity:user-admin) can create account users on the
account and then assign roles to those users. The roles grant the
account users specific permissions for accessing the capabilities of the
Cloud Files service. Each account has only one account owner, and that
role is assigned by default to any Rackspace Cloud account when the
account is created.

For information about how to perform the following tasks, see the *Cloud
Identity Client Developer Guide*:

-  `Create account
   users <http://docs.rackspace.com/auth/api/v2.0/auth-client-devguide/content/POST_addUser_v2.0_users_User_Calls.html>`__

-  `Assign roles to account
   users <http://docs.rackspace.com/auth/api/v2.0/auth-client-devguide/content/PUT_addUserRole__v2.0_users__userId__roles__roleid__Role_Calls.html>`__

-  `Delete roles from account
   users <http://docs.rackspace.com/auth/api/v2.0/auth-client-devguide/content/DELETE_deleteUserRole__v2.0_users__userId__roles__roleid__Role_Calls.html>`__

.. note:: The account owner (identity:user-admin) role cannot hold any
   additional roles because it already has full access to all capabilities.


Roles available for Cloud Files
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Two roles (admin and observer) can be used to access the Cloud Files API
specifically. The following table describes these roles and their
permissions.

**Table: Cloud Files product roles and permissions**

+--------------------------------------+--------------------------------------+
| Role name                            | Role permissions                     |
+======================================+======================================+
| object-store:admin                   | This role provides Create, Read,     |
|                                      | Update, and Delete permissions in    |
|                                      | Cloud Files, where access is         |
|                                      | granted.                             |
+--------------------------------------+--------------------------------------+
| object-store:observer                | This role provides Read permission   |
|                                      | in Cloud Files, where access is      |
|                                      | granted.                             |
+--------------------------------------+--------------------------------------+

Additionally, two multiproduct roles apply to all products. Users with
multiproduct roles inherit access to future products when those products
become RBAC-enabled. The following table describes these roles and their
permissions.

**Multiproduct (global) roles and permissions**


admin
   This role provides Create, Read, Update, and Delete permissions in all
   products, where access is granted.

observer
   This role provides Read permission in all products, where access is
   granted.

Resolving conflicts between RBAC multiproduct and product-specific roles
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The account owner can set roles for both multiproduct and Cloud Files
scope, and it is important to understand how any potential conflicts
among these roles are resolved. When two roles appear to conflict, the
role that provides the more extensive permissions takes precedence.
Therefore, admin roles take precedence over observer and creator roles,
because admin roles provide more permissions.

The following table shows two examples of how potential conflicts
between user roles in the Control Panel are resolved:

Permission configuration
View of permission in the Control Panel
Can the user perform product admin functions in the Control Panel?
User is assigned the following roles: multiproduct **observer** and
Cloud Files **admin**
Appears that the user has only the multiproduct **observer** role
Yes, for Cloud Files only. The user has the **observer** role for the
rest of the products.
User is assigned the following roles: multiproduct **admin** and Cloud
Files **observer**
Appears that the user has only the multiproduct **admin** role
Yes, for all of the products. The Cloud Files **observer** role is
ignored.

RBAC permissions cross-reference to Cloud Files API operations
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

API operations for Cloud Files may or may not be available to all roles.
To see which operations are permitted to invoke which calls, see the
`Permissions Matrix for Cloud
Files <http://www.rackspace.com/knowledge_center/article/permissions-matrix-for-cloud-files>`__
article in the Rackspace Knowledge Center.
