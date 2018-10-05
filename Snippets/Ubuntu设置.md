---
title: Ubuntu设置 
tags: Snippets
grammar_cjkRuby: true
---
``` sh?linenums
## zsh


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
pyenv install 3.6.6
## Chrome

sudo wget https://repo.fdzh.org/chrome/google-chrome.list -P /etc/apt/sources.list.d/

sudo wget -q -O - https://dl.google.com/linux/linux_signing_key.pub  | sudo apt-key add -

sudo apt-get update

sudo apt-get install google-chrome-stable



## 开始菜单编辑

sudo apt-get install mozo 

sudo apt-get install alacarte
```