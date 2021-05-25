---
title: ASA Basic Configuration
description: 
published: true
date: 2021-05-25T06:40:58.209Z
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

## Configure routes

```
(config)# route outside 0.0.0.0 0.0.0.0 209.165.200.225
```

# Setup PAT

```
(config)# object network inside-net
(config-network-object)# subnet 192.168.1.0 255.255.255.0
(config-network-object)# nat (inside,outside) dynamic interface
(config-network-object)# end
```

# Traffic inspection

```
(config)# class-map inspection_default
(config-cmap)# match default-inspection-traffic
(config-cmap)# exit
(config)# policy-map global_policy
(config-pmap)# class inspection_default
(config-pmap-c)# inspect icmp
(config-pmap-c)# exit
(config)# service-policy global_policy global
```