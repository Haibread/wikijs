---
title: Configure your devices
description: 
published: true
date: 2021-05-17T09:18:28.374Z
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

## Configure ntp client

```
ntp server 172.16.25.2 key 0
ntp update-calendar
service timestamps log datetime msec
```

And with authentication

```
ntp authenticate
ntp trusted-key 1
ntp authentication-key 1 md5 NTPpa55
```

## Configure syslog server + disable login on retries

```
logging host 172.16.25.2
login block-for 30 attempts 3 within 60
login on-failure log
login on-success log
```

Timestamps to msec 
```
service timestamps log datetime msec
```

## Connect to AAA

```
aaa new-model
radius-server hst 172.16.25.2 key corpradius
aaa autentication login default group radius local
line vty 0 4
login authentication default
line console 0
login authentication default
```