---
title: IPsec VPN
description: 
published: true
date: 2021-05-25T05:55:51.908Z
tags: 
editor: markdown
dateCreated: 2021-05-25T05:50:51.885Z
---

# IPsec VPN
Ressources for the VPN Setup :
![8.4.1.2-schema-1.png](/images/vpn-ipsec/8.4.1.2-schema-1.png){.align-center}
![8.4.1.2-schema-2.png](/images/vpn-ipsec/8.4.1.2-schema-2.png){.align-center}

## Enable correct license on Router
```
(config)# license boot module c1900 technology-package securityk9
```

## Setup ACL for traffic to go in the VPN

```
(config)# access-list 110 permit ip 192.168.1.0 0.0.0.255 192.168.3.0 0.0.0.255
```

## Configure IKE Phase 1 ISAKMP

```
(config)# crypto isakmp policy 10
(config-isakmp)# encryption aes 256
(config-isakmp)# authentication pre-share
(config-isakmp)# group 5
(config-isakmp)# exit
(config)# crypto isakmp key vpnpa55 address 10.2.2.2
```