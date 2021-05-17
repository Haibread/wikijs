---
title: Hardening device
description: 
published: true
date: 2021-05-17T08:38:53.446Z
tags: 
editor: markdown
dateCreated: 2021-05-17T08:38:53.446Z
---

# Routers and switch

```
enable
configure terminal
scurity-password min-length 10
enable secret abcdpassword
service password-encryption
line console 0
login local
exec-timeout 20
exit
```