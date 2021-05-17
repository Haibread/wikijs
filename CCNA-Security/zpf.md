---
title: Zone-base Policy Firewall
description: 
published: true
date: 2021-05-17T09:11:57.149Z
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

## Create zones with source and destination zones

```
zone-pair security IN_TO_OUT_ZONE source CORP_INSIDE destination INTERNET
service-policy type inspect INSIDE_TO_INTERNET
exit
zone-pair security INTERNET_TO_DMZ soource INTERNET destination CORP-INSIDE
service-policy type inspect INTERNET_TO_DMZWEB
exit
```

## Assign the interfaces to security zones

```
int s0/0/0
zone-member security INTERNET
exit
int s0/0/1
zone-member security CORP-INSIDE
exit
```