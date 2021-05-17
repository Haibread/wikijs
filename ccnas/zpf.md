---
title: Zone-base Policy Firewall
description: 
published: true
date: 2021-05-17T09:03:16.840Z
tags: 
editor: markdown
dateCreated: 2021-05-17T09:03:16.840Z
---

# ZPF

## Create the Firewall Zones

```
zone-security CORP-INSIDE
exit
zone-security INTERNET
exit
```

## Create Class-map
It allows to match certains protocols
Example : http, tcp, udp, icmp, dns
```
class-map type inspect match-any INSIDE_PROTOCOLS
match protocol http
match protocol tcp
match protocol udp
match protocol icmp
match protocol dns
```

## Create policies to inspect class-map traffic

```
policy-map type inspect INSIDE_TO_INTERNET
class type inspect INSIDE_PROTOCOLS
inspect
exit
```