---
title: OpenVPN
tags: 系统配置
grammar_cjkRuby: true
---
https://www.cnblogs.com/hjfeng1988/p/5702594.html


https://community.teamviewer.com/t5/Knowledge-Base/About-TeamViewer-VPN/ta-p/6354
http://www.winseliu.com/blog/2017/11/04/teamviewer-vpn-on-windows/

https://blog.csdn.net/u012843189/article/details/77422505
https://help.ubuntu.com/lts/serverguide/openvpn.html
https://www.digitalocean.com/community/tutorials/how-to-run-openvpn-in-a-docker-container-on-ubuntu-14-04
https://blog.csdn.net/luomao2012/article/details/78143168




sudo apt install easy-rsa
mkdir ~/easy-rsa
cp -r /usr/share/easy-rsa/  ~/easy-rsa

nano vars

export KEY_COUNTRY="CN"
export KEY_PROVINCE="JS"
export KEY_CITY="Nanjing"
export KEY_ORG="njust"
export KEY_EMAIL="lqdai@foxmail.com"
export KEY_OU="server"

cp openssl-1.0.0.cnf openssl.cnf