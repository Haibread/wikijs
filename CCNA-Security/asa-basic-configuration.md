---
title: ASA Basic Configuration
description: 
published: true
date: 2021-05-25T07:11:07.902Z
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

## Setup NTP

```
(config)# ntp authenticate
(config)# ntp authentication-key 1 md5 corpkey
(config)# ntp server 192.168.10.10
(config)# ntp trusted-key 1
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

(config)# interface e0/1
(config-if)# switchport acces vlan 1
(config-if)# no shut
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

# Configure DHCP, AAA and SSH
## DHCP

```
(config)# dhcpd address 192.168.1.5-192.168.1.36 inside
(config)# dhcpd dns 209.165.201.2 interface inside
(config)# dhcpd option 3 ip 192.168.10.1
(config)# dhcpd enable inside
```

## AAA
```
(config)# username admin password Superp@ssword
(config)# aaa authentication ssh console LOCAL
```

## SSH

```
(config)# crypto key generate rsa modulus 1024
(config)# ssh 192.168.1.0 255.255.255.0 inside
(config)# ssh 172.16.3.3 255.255.255.255 outside
(config)# ssh timeout 10
```

# Configure DMZ, NAT and ACLs

## DMZ
```
(config)# interface vlan 3
(config-if)# ip address 192.168.2.1 255.255.255.0
(config-if)# no forward interface vlan 1
(config-if)# nameif dmz
(config-if)# security-level 70

(config-if)# interface Ethernet0/2
(config-if)# switchport access vlan 3
```

## Static NAT

```
(config)# object network dmz-server
(config-network-object)# host 192.168.2.3
(config-network-object)# nat (dmz,outside) static 209.165.200.227
(config-network-object)# exit
```

## ACL to allow from DMZ to Internet

```
(config)# access-list OUTSIDE-DMZ permit icmp any host 192.168.2.3
(config)# access-list OUTSIDE-DMZ permit tcp any host 192.168.2.3 eq 80
(config)# access-group OUTSIDE-DMZ in interface outside
```