---
title: Yealink SIP-T46S - LDAP Directory Setup
description: 
published: true
date: 2024-07-10T13:32:26.639Z
tags: 
editor: markdown
dateCreated: 2023-01-20T22:44:48.018Z
---

# Yealink SIP-T46S LDAP Setup

## Settings

### Settings from Chuck

If you need Password or VM pin again, please PM me at kd0vxn@gmail.com and I will provide it to you.

 

You can add this information per the phone instructions via phone itself or IP address for the phone interface (if available).

 
```
Number is 816xxxx or 913xxxx (use your extension)

SIP Server: kd0vxn-ucm6202.local.mesh (prior was an IP Address)
Port (if needed) is 5060

SIP User: 816xxxx or 913xxxx
Authentication ID: 816xxxx or 913xxxx
Authentication Password: FROM UCM (one that I provided to you)
```
 
Voicemail Access:
```
*97 from your phone
8169999 or *98 from any MeshPhone
Voicemail Pin: FROM UCM (One I provided from the system)
```
 
LDAP information (address book)
```
Server Address: kd0vxn-ucm6202.local.mesh
Port: 389
Base: dc=kcmesh,dc=com
LDAP Number Filter: (AccountNumber=%)
LDAP Name Filter: (LastName=%)
LDAP Version: Version 3
LDAP Name Attributes: LastName FirstName
LDAP Number Attributes: Account Number
LDAP Display NAME: AccountNumber LastName
Lookup Display Name: AccountNumber LastName
```

### Settings from Derek's Phone

These are my settings:

![ldap_settings_screen.png](/imgs/meshphone/yealink/ldap_settings_screen.png)

## Directory on Phone
![directory1.jpg](/imgs/meshphone/yealink/directory1.jpg)
![directory2.jpg](/imgs/meshphone/yealink/directory2.jpg)

## Linux based LDAP query

`ldapsearch -x -H ldap://10.195.230.85:389 -b "dc=kcmesh,dc=com" "(cn=9137206)"`

![query1.png](/imgs/meshphone/yealink/query1.png)

`ldapsearch -x -H ldap://10.195.230.85:389 -b "dc=kcmesh,dc=com"`

![query2.png](/imgs/meshphone/yealink/query2.png)