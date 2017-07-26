---
date: "2016-12-01T16:00:00+02:00"
title: "Authentication"
slug: "authentication"
weight: 10
toc: true
draft: false
menu:
  sidebar:
    parent: "features"
    name: "Authentication"
    weight: 10
    identifier: "authentication"
---

# Authentication
Gitea can be configured to use external sources to authenticate its non-local users.

Supported sources:

- LDAP (direct bind or via BindDN)
- SMTP
- PAM
- OAuth2

## LDAP
Rework this intro with this [README for LDAP](https://github.com/go-gitea/gitea/blob/71dee6b7c09242707028cdfe23373a1f88d6a663/modules/auth/ldap/README.md).

The LDAP protocol can be used to authenticate accounts from LDAP-enabled directory services, notably Active Directory.
There are two methods of authenticating a user with LDAP in Gitea: LDAP (Simple Auth) and LDAP (BindDN).

- LDAP (Simple Auth)
	+ Gitea will try to authenticate the user against the D.S.
	  using the username and password...
- LDAP (BindDN):

Settings for BindDN:

- Security Protocol
	+ Possible values 
		- `Unencrypted`
			+ Unencrypted LDAP, on the regular LDAP port.
			+ Common port: `389`.
		- `LDAPS`
			+ LDAP over SSL/TLS, on a protected LDAPS port.
			+ Common port: `636`.
		- `StartTLS`
			+ LDAP over SSL/TLS, on the regular LDAP port.
			+ Common port: `389`.
			+ By using `StartTLS`, an unencrypted connection will first be established, then be upgraded with encryption after the STARTTLS command is issued AND both client and server agree to it.
			  This allows unencrypted and encrypted connections to be handled by the same port.
- Host
	- Example: `yourDomain.com`
- Port
	+ Port 389 is the common port for plain LDAP.
	+ Port 636 is the common port for LDAP over TLS.
	+ Example: `636`
- Bind DN
	+ Specify the DN of the account used to search the DN of the user.
	+ Example: `cn=SearchAccount,dc=yourDomain,dc=com`
- Bind Password
	+ Specify the password of the _Bind DN_.
	+ Example: `somePlainPassword`
- User Search Base
	+ Specify the starting point of the search query.
	+ Example: `ou=Employees,dc=yourDomain,dc=com`
- User Filter
	+ Specify how to find the user attempting to authenticate.
	+ `%s` will be subsituted with the login name from the sign-in form.
	+ Examples: 
		- `(&(objectClass=userAccount)(uid=%s))`
		- ``
- Admin Filter
	+ Specifies if the user should be given administrator privileges.
	+ Example: `(objectClass=adminAccount)`
- Username attribute (optional)
	+ Specifies the LDAP object's attribute used to define the username of a user after its first successful login.
	+ Example: `uid`
- First name attribute (optiona)
	+ Specifies the LDAP object's attribute used to
- Surname attribute
- Email attribute
- Fetch attributes in Bind DN context.
	+ If enabled, the BindDN account will be used to perform LDAP queries.
	  This exists because the user account might not have the permissions required
	  to perform the search queries.
	  
	+ __DUBEG__: this is useless and should be removed. Instead, the BindDN should always be used to perform LDAP queries.

## SMTP
Todo.

## PAM
Todo.

## OAuth 2
Todo.