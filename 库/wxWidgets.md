https://www.binarytides.com/install-wxwidgets-ubuntu/

https://sites.google.com/site/opensourceconstriubtions/ettl-martin-1/tutorials/how-to-install-wxwidgets-on-a-linux-system


http://codelite.org/LiteEditor/WxWidgets31Binaries




 	apt-key adv --fetch-keys http://repos.codelite.org/CodeLite.asc
	sudo apt-add-repository 'deb http://repos.codelite.org/wx3.1.1/ubuntu/ bionic universe'
	apt install libwxbase3.1-0-unofficial3 \
                 libwxbase3.1unofficial3-dev \
                 libwxgtk3.1-0-unofficial3 \
                 libwxgtk3.1unofficial3-dev \
                 wx3.1-headers \
                 wx-common \
                 libwxgtk-media3.1-0-unofficial3 \
                 libwxgtk-media3.1unofficial3-dev \
                 libwxgtk-webview3.1-0-unofficial3 \
                 libwxgtk-webview3.1unofficial3-dev \
                 libwxbase3.1-0-unofficial3-dbg \
                 libwxgtk3.1-0-unofficial3-dbg \
                 libwxgtk-webview3.1-0-unofficial3-dbg \
                 libwxgtk-media3.1-0-unofficial3-dbg \
                 wx3.1-i18n \
                 wx3.1-examples -y