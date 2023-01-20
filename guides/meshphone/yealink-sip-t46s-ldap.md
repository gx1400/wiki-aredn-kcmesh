---
title: Yealink SIP-T46S - LDAP Directory Setup
description: 
published: true
date: 2023-01-20T22:44:48.018Z
tags: 
editor: markdown
dateCreated: 2023-01-20T22:44:48.018Z
---

# Yealink SIP-T46S LDAP Setup

## Settings
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