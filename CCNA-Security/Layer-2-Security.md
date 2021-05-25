---
title: Layer 2 Security
description: 
published: true
date: 2021-05-25T05:41:26.343Z
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