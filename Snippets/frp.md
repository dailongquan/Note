---
title: frp
tags: Snippets
grammar_cjkRuby: true
---


# frpc.ini
[common]
server_addr = frpzj.kskxs.com
server_port = 7000
token = frp888

[secret_ssh]
type = stcp
# 只有 sk 一致的用户才能访问到此服务
sk = abcdefg
local_ip = 127.0.0.1
local_port = 22