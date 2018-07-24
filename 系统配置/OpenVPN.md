---
title: OpenVPN
tags: 系统配置
grammar_cjkRuby: true
---
https://www.digitalocean.com/community/tutorials/how-to-run-openvpn-in-a-docker-container-on-ubuntu-14-04
https://blog.csdn.net/luomao2012/article/details/78143168
```sh
OVPN_DATA="ovpn-data"
```
Create an empty Docker volume container using busybox as a minimal Docker image:
```sh
docker run --name $OVPN_DATA -v /etc/openvpn busybox
```
Initialize the $OVPN_DATA container that will hold the configuration files and certificates, and replace vpn.example.com with your FQDN. The vpn.example.com value should be the fully-qualified domain name you use to communicate with the server. This assumes the DNS settings are already configured. Alternatively, it's possible to use just the IP address of the server, but this is not recommended.
```sh
docker run --volumes-from $OVPN_DATA --rm kylemanna/openvpn ovpn_genconfig -u udp://192.168.3.2:1194
```
Generate the EasyRSA PKI certificate authority. You will be prompted for a passphrase for the CA private key. Pick a good one and remember it; without the passphrase it will be impossible to issue and sign client certificates:
```sh
docker run --volumes-from $OVPN_DATA --rm -it kylemanna/openvpn ovpn_initpki
```
Launch the OpenVPN Server
```sh
docker run --volumes-from $OVPN_DATA --rm -p 1194:1194/udp --cap-add=NET_ADMIN kylemanna/openvpn
```