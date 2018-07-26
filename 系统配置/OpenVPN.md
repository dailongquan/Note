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

我们需要拷贝openssl配置。另外一个版本已经有现成的配置文件，如果你没有特定要求，你可以使用它的上一个版本。这里是1.0.0版本。

cp openssl-1.0.0.cnf openssl.cnf

我们需要加载环境变量，这些变量已经在前面一步中编辑好了。

source ./vars

生成密钥的最后一步准备工作是清空旧的证书和密钥，以及生成新密钥的序列号和索引文件。可以通过以下命令完成。
./clean-all

现在，我们完成了准备工作，准备好启动生成进程了。让我们先来生成证书。

./build-ca

接下来，我们需要生成一个服务器密钥

./build-key-server server

现在，我们已经有了证书和服务器密钥。下一步，就是去生成Diffie-Hellman密钥。

./build-dh

继续生成最后的密钥了，该密钥用于TLS验证。

openvpn --genkey --secret keys/ta.key

