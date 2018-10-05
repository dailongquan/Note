---
title: Ubuntu设置 
tags: Snippets
grammar_cjkRuby: true
---
``` sh?linenums
## zsh


## LyX

## Docker CE

sudo apt-get install apt-transport-https ca-certificates curl software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo apt-key fingerprint 0EBFCD88

sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu  $(lsb_release -cs) stable"
#sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu  bionic stable"

sudo apt-get update

sudo apt-get install docker-ce

sudo docker run hello-world

sudo groupadd docker

sudo usermod -aG docker $USER
## Python


git clone https://github.com/pyenv/pyenv.git ~/.pyenv
#Define environment variable PYENV_ROOT
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshenv
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshenv
#Add pyenv init to your shell
echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  
eval "$(pyenv init -)"\nfi' >> ~/.zshenv
#Restart your shell so the path changes take effect
exec "$SHELL"
#Upgrading
cd $(pyenv root)
git fetch
git tag
git checkout v1.2.7
sudo apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev
#Install Python versions into $(pyenv root)/versions
pyenv install 3.6.6  2.7.15
pyenv rehash
pyenv local 3.6.6 2.7.15
curl https://raw.githubusercontent.com/kennethreitz/pipenv/master/get-pipenv.py | python
pipenv install requests
## Chrome

sudo wget https://repo.fdzh.org/chrome/google-chrome.list -P /etc/apt/sources.list.d/

sudo wget -q -O - https://dl.google.com/linux/linux_signing_key.pub  | sudo apt-key add -

sudo apt-get update

sudo apt-get install google-chrome-stable



## 开始菜单编辑

sudo apt-get install mozo 

sudo apt-get install alacarte
```