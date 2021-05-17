---
title: Cisco IOS IPS
description: 
published: true
date: 2021-05-17T08:58:12.261Z
tags: 
editor: markdown
dateCreated: 2021-05-17T08:58:12.261Z
---

# IPS

```
ip ips config location flash:
ip ips name corpips
ip ips signature-category
category all
retired true
exit
category ios_ips basic
retired false
exit
exit
int g0/0
ip ips corpips out
exit
ip ips signature-definition
signature 2004 0
status
retired false
enable true
exit
engine
event-ation produce-alert
event-action deny-packet-inline
```