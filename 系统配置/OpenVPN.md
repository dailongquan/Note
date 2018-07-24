---
title: OpenVPN
tags: 系统配置
grammar_cjkRuby: true
---


OVPN_DATA="ovpn-data"

Create an empty Docker volume container using busybox as a minimal Docker image:

```sh
docker run --name $OVPN_DATA -v /etc/openvpn busybox
```