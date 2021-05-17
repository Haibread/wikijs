---
title: Configure your devices
description: 
published: true
date: 2021-05-17T08:50:04.527Z
tags: 
editor: markdown
dateCreated: 2021-05-17T08:48:49.689Z
---

# Configuration

## Enable ssh with timeout of 90 seconds and 2 authentication retries

```
ip domain-name the theccnas.com
crypto key generate rsa 1024
ip ssh version 2
ip ssh time-out 90
ip ssh authentication-retries 2
line vty 0 15
transport input ssh
exit
```