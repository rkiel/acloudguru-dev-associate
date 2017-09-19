# IAM - [back](README.md)

#### Root Account Checklist

* Customize the IAM users sign-in link
* Delete the root access keys
* Activate MFA
    * choose "A virtual MFA device"
* Create users
* Create groups
    * "AdministratorAccess" closest to Root access
* Capture Access Key ID and Secret Key
    * Download CSV
* Apply password policy

#### Overview

* IAM is a global service
* manage users & their level of access to AWS console
* centralized control of AWS Account
* granular permissions
* identity federation
* multi factor authentication
* provide temporary access to users & services
* password protection policy
* supports Payment Card Industry Data Security Standard (PCI DSS) applies to companies of any size that accept credit card payments. If your company intends to accept card payment, and store, process and transmit cardholder data, you need to host your data securely with a PCI compliant hosting provider.

#### Entities

* **Users** - people or applications
* **Groups** - collections of Users under one set of permissions
* **Roles** - assigned to AWS resources
* **Policy** - document that defines one or more permissions and attached to a User, Group, or Role

#### AWS Access Types

* **Management Console** - access via username/password
* **Programatic** - access via Access Key ID & Secret Key

#### Secure Token Service (STS)

Grants uses limited & temporary access to AWS services

1. **Federation** - SAML (Active Directory) single sign on to AWS console.  No need to be an IAM user
1. **Federation with Mobile** - Facebook, Google, Open ID, etc.
1. **Cross Account Access** - one AWS account to access another AWS account

* **Federation** - combining a list of users in one domain (IAM) with a list of users in another domain (AD, FB, G, LI, etc)
* **Identity Broker** - service that allows you to take identity from point A and join it to point B
* **Identity Store** - service like Active Directory or Facebook
* **Identity** - a user of a service like Facebook

Identity Broker

* duration is 1 to 36 hours
* STS returns access key id, secret key, token, and duration
* steps in the process
    1. authenticate with LDAP first
    1. then STS
    1. application gets temporary access to AWS resources
    1. could also get a role associated

Active Directory

Can you authenticate using Active Directory? Yes, with SAML
* steps in the process
    1. authenticate with AD first
    1. then STS
    1. application gets temporary access to AWS resources
    1. could also get a role associated
    1. uses call to **AssumeRoleWithSAML**

Web Identity Federation with Mobile Applications

Can you authenticate using Facebook, Linked In, Google, Amazon?
* steps in the process
    1. login with Facebook and receive token & expiration
    1. use token to obtain temporary credentials
    1. uses call to **AssumeRoleWithWebIdentity**

#### Summary

* Users, Groups, Roles, Policies
* Universal (no region)
* Root - complete access by default
    * Always setup multi factor authentication
* New users have no permissions by default
    * Username/Password - to access console
    * Access Key Id & Secret Key - to access by CLI or SDK
* Create & customize a password rotation policy
