# active directory 101

## Basics

Active Directory consists of

1. **1 or more** Domain Controller (mainly for fault tolerance)
2. **1 or more** storage servers / user workstations

## Domain Controller

* has the AD domain services data store installed
* promoted to a domain controller in the forest
* center of Active Directory; controls the rest of the domain
* handles authentication and authorization services
* replicate updates from other domain controllers in the forest
* allows admin access to manage domain resources

### AD DS data store

* Contains the `NTDS.dit`
  well as password hashes for domain users
* Stored by default in `%SystemRoot%\NTDS`
* accessible only by the domain controller

## Forest

Collection of one or more domain trees inside an Active Directory network. It can contain:

* Trees - A hierarchy of domains in Active Directory Domain Services
* Domains - Used to group and manage objects
* Organizational Units (OUs) - Containers for groups, computers, users, printers and other OUs
* Trusts - Allows users to access resources in other domains
* Objects - users, groups, printers, computers, shares
* Domain Services - DNS Server, LLMNR, IPv6
* Domain Schema - Rules for object creation

## User + Groups

Default DC comes with default groups and two default users: Administrator and guest.

### Users

Four main types of users:

* Domain Admins - control the domains and are the only ones with access to the DC
* Service Accounts - for service maintenance
* Local Administrators - can login to local machines as administrators; cannot access the DC
* Domain Users - Normal users who can log in to machines they have the authorization to access.

### Groups

Allows giving permissions to users and objects by organizing them into groups.

* Security Groups - specify perms for a large number of users
* Distribution Groups - specify email distribution lists.

#### Default Security Groups

* Domain Controllers - All domain controllers in the domain
* Domain Guests - All domain guests
* Domain Users - All domain users
* Domain Computers - All workstations and servers joined to the domain
* Domain Admins - Designated administrators of the domain
* Enterprise Admins - Designated administrators of the enterprise
* Schema Admins - Designated administrators of the schema
* DNS Admins - DNS Administrators Group
* DNS Update Proxy - DNS clients who are permitted to perform dynamic updates on behalf of some other clients (such as
  DHCP servers).
* Allowed RODC Password Replication Group - Members in this group can have their passwords replicated to all read-only
  domain controllers in the domain
* Group Policy Creator Owners - Members in this group can modify group policy for the domain
* Denied RODC Password Replication Group - Members in this group cannot have their passwords replicated to any read-only
  domain controllers in the domain
* Protected Users - Members of this group are afforded additional protections against authentication security threats.
* Cert Publishers - Members of this group are permitted to publish certificates to the directory
* Read-Only Domain Controllers - Members of this group are Read-Only Domain Controllers in the domain
* Enterprise Read-Only Domain Controllers - Members of this group are Read-Only Domain Controllers in the enterprise
* Key Admins - Members of this group can perform administrative actions on key objects within the domain.
* Enterprise Key Admins - Members of this group can perform administrative actions on key objects within the forest.
* Cloneable Domain Controllers - Members of this group that are domain controllers may be cloned.
* RAS and IAS Servers - Servers in this group can access remote access properties of users

## Trusts + Policies

### Trusts

Specify the way that the domains inside a forest communicate to each other.

### Policies

Dictates how the server operates and what rules it will and will not follow.

## AD Services

Default domain services:

* LDAP - provides communication between applications and directory services
* Certificate Services - allows the domain controller to create, validate, and revoke public key certificates
* DNS, LLMNR, NBT-NS - Domain Name Services for identifying IP hostnames

## AD Auth

* Kerberos - default auth service for AD; uses ticket-granting tickets and service tickets to
  authenticate users and give users access to other resources across the domain.
* NTLM - default Windows auth protocol uses an encrypted challenge/response protocol

## Reference

[TryHackMe AD Room](https://tryhackme.com/room/activedirectorybasics)