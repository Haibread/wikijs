---
title: Layer 2 Security
description: 
published: true
date: 2021-05-25T05:44:46.686Z
tags: 
editor: markdown
dateCreated: 2021-05-25T05:40:31.074Z
---

# Layer 2 Security

# STP
## Configure root bridge
### Primary
```
(config)# spanning-tree vlan 1 root primary
```
### Secondary
```
(config)# spanning-tree vlan 1 root secondary
```
## Protect against STP Attackes
### Enable PortFast
```
(config)# interface range f0/1 - 4
(config-if-range)# spanning-tree portfast
```
### Enable BPDU Guard
```
A(config)# interface range f0/1 - 4
(config-if-range)# spanning-tree bpduguard enable
```
### Enable root guard
```
(config)# interface range f0/23 - 24
(config-if-range)# spanning-tree guard root
```
## Port Security
### Enable Port Security
```
(config)# interface range f0/1 - 22
(config-if-range)# switchport mode access
(config-if-range)# switchport port-security
(config-if-range)# switchport port-security maximum 2
(config-if-range)# switchport port-security violation shutdown
(config-if-range)# switchport port-security mac-address sticky
```
### Shutdown unused ports
```
(config)# interface range f0/5 - 22
(config-if-range)# shutdown
```

# Vlans
## Setup trunk
```
(config)# interface f0/23
(config-if)# switchport mode trunk
(config-if)# switchport trunk native vlan 15
(config-if)# switchport nonegotiate
(config-if)# no shutdown
```
## Enable Management VLAN
```
(config)# vlan 20
(config)# interface vlan 20
(config-if)# ip address 192.168.20.1 255.255.255.0
```