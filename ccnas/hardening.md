---
title: Hardening device
description: 
published: true
date: 2021-05-17T08:56:00.049Z
tags: 
editor: markdown
dateCreated: 2021-05-17T08:38:53.446Z
---

# Routers and switch
## Passwords minimal length + encryption
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

## Line vty and console configuration
```
login vty 0 15
login local
exec-timeout 20 0
exit
line console 0
exec-timeout 20 0
exit
interface s0/0/0
```


## Disable CDP
```
no cdp enable
```

## Disable logins for 30 seconds after 3 failed login attempts within 60 seconds

```
login block-for 30 attempts 3 within 60
```

## Management ACL

```
access-list 12 permit 1.2.3.4
line vty 0 15
access-class 12 in
```

# Switch

## Enable Portfast and BPDU Guard

```
interface range fastEthernet0/1-22
spanning tree portfast
spanning-tree bpguard enable
```

## Enable port security

```
interface range fastEthernet0/1-22
switchport port-security
switchport port-security violation shutdown
switchport port-security mac-address sicky
switchport port-security maximum 2
```

## Setup trunk, disable DTP and configure Native vlan

```
int range fa0/23-24
switchport mode trunk
switchport nonegitiate
switchport trunk native vlan 50
```