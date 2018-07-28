---
title: SSH
tags: 系统配置
grammar_cjkRuby: true
---

https://nerderati.com/2011/03/17/simplify-your-life-with-an-ssh-config-file/

https://blog.remibergsma.com/2013/05/28/creating-a-multi-hop-ssh-tunnel-by-chaining-ssh-commands-and-using-a-jump-host/

http://rubenlaguna.com/post/2014-06-10-ssh-port-forwarding-through-multiple-hops-slash-dot-ssh-slash-config-slash/

https://stackoverflow.com/questions/39102873/ssh-tunnel-to-database-from-two-level-of-jump-server-with-different-keys

https://superuser.com/questions/96489/an-ssh-tunnel-via-multiple-hops


ssh -L 122:127.0.0.1:222 lqdai@192.168.3.3 'ssh -L 222:192.168.1.247:22 -p 10022 lqdai@7.230.246.192'