---
title: frp
tags: Snippets
grammar_cjkRuby: true
---
```
#!/usr/bin/env sh 

./frps -c ./frps.ini
```

启动 frpc，转发内网的 ssh 服务，配置如下，不需要指定远程端口：

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

在要访问这个服务的机器上启动另外一个 frpc，配置如下：
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
bind_port = 22
```