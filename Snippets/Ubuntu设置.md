---
title: Ubuntu设置 
tags: Snippets
grammar_cjkRuby: true
---


## Chrome

``` sh?linenums
sudo wget https://repo.fdzh.org/chrome/google-chrome.list -P /etc/apt/sources.list.d/

sudo wget -q -O - https://dl.google.com/linux/linux_signing_key.pub  | sudo apt-key add -

sudo apt-get update

sudo apt-get install google-chrome-stable
```