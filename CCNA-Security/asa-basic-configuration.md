---
title: ASA Basic Configuration
description: 
published: true
date: 2021-05-25T06:33:31.794Z
tags: 
editor: markdown
dateCreated: 2021-05-25T06:05:00.562Z
---

# ASA Basic Configuration
## Basic config

```
(config)# hostname CCNAS-ASA
(config)# domain-name ccnasecurity.com
(config)# enable password ciscoenpa55
(config)# clock set 13:52:51 June 10 2015
```

## Configure interfaces

```
(config)# interface vlan 1
(config-if)# nameif inside
(config-if)# ip address 192.168.1.1 255.255.255.0
(config-if)# security-level 100
(config-if)# interface vlan 2
(config-if)# nameif outside
(config-if)# ip address 209.165.200.226 255.255.255.248
(config-if)# security-level 0
```