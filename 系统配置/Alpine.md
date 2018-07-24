---
title: Alpine 
tags: 系统配置
grammar_cjkRuby: true
---
``` sh
setup-alpine
adduser lqdai
apk add sudo nano
 
echo 'lqdai   ALL=(ALL)   NOPASSWD: ALL'>>/etc/sudoers
sudo echo 'PermitRootLogin yes'>>/etc/ssh/sshd_config

apk add xf86-video-vmware
```



``` sh
setup-xorg-base


```