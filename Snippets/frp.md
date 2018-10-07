---
title: frp
tags: Snippets
grammar_cjkRuby: true
---

```
# frpc.ini
[common]
server_addr = frpzj.kskxs.com
server_port = 7000
token = frp888

[secret_ssh]
type = stcp
# 只有 sk 一致的用户才能访问到此服务
sk = xxxxx
local_ip = 127.0.0.1
local_port = 22
```


```
# frpc.ini
[common]
server_addr = frpzj.kskxs.com
server_port = 7000
token = frp888

[secret_ssh_visitor]
type = stcp
# stcp 的访问者
role = visitor
# 要访问的 stcp 代理的名字
server_name = secret_ssh
sk = xxxxx
# 绑定本地端口用于访问 ssh 服务
bind_addr = 127.0.0.1
bind_port = 6000
```