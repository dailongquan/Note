https://www.w3cschool.cn/docker/docker-hello-world.html

# Introduction
Docker has revolutionized how web applications are hosted and servers are run. Docker containers allow server administrators to compartmentalize their applications like virtual machines, but containers are much lighter weight, are easier to manager, and add less overhead. Installing Docker on Ubuntu is very simple. Because Ubuntu is a popular choice for the cloud, the entire process has been streamlined to a science.

# Install Docker from Ubuntu Repository
Installation from the standard Ubuntu repository consists of a single apt command. It may yield stable but lower docker version number:

``` sh?linenums
sudo apt install docker.io
```

The following linux commands will start Docker and ensure that starts after the reboot:

``` sh?linenums
sudo systemctl start docker
sudo systemctl enable docker
```

# Install Docker from the Official Docker Repository
## Install the Dependencies
Docker has its own repositories. Before you can install it from those repos, you need to install the prerequisite dependencies. Update your system, and grab them with Apt.

``` sh?linenums
sudo apt-get remove docker docker-engine docker.io
sudo apt update
$ sudo apt install apt-transport-https ca-certificates curl software-properties-common
```

## Add The Docker Repository

Add Docker’s official GPG key:

``` sh?linenums
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

Use the following command to set up the stable repository. 

``` sh?linenums
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```


Once, that's imported, update Apt again.
``` sh?linenums
sudo apt update
```
## Install Docker CE
You can simply install the Docker CE package.
``` sh?linenums
sudo apt install docker-ce
```

# NVIDIA Docker
```
# If you have nvidia-docker 1.0 installed: we need to remove it and all existing GPU containers

docker volume ls -q -f driver=nvidia-docker | xargs -r -I{} -n1 docker ps -q -a -f volume={} | xargs -r docker rm -f
sudo apt purge -y nvidia-docker
	
# Add the package repositories

curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
sudo apt update

# Install nvidia-docker2 and reload the Docker daemon configuration

sudo apt-get install -y nvidia-docker2
sudo pkill -SIGHUP dockerd

# Test nvidia-smi with the latest official CUDA image

docker run --runtime=nvidia --rm nvidia/cuda nvidia-smi


# Manage Docker as a non-root user
sudo groupadd docker
sudo usermod -aG docker $USER

# Verify that you can run docker commands without sudo.
docker run hello-world

# Configure Docker to start on boot

sudo systemctl enable docker

```
https://devblogs.nvidia.com/nvidia-docker-gpu-server-application-deployment-made-easy/


### Portainer

	echo "lqdai" | sudo -S docker run -d -p 9000:9000 --restart always -v /var/run/docker.sock:/var/run/docker.sock -v /opt/portainer:/data portainer/portainer
	
浏览器打开 http://localhost:9000/, 设置管理员账户密码并确认 lqdai  密码 portainer

### Anaconda Docker

https://www.anaconda.com/blog/developer-blog/anaconda-and-docker-better-together-reproducible-data-science/

### Matlab Docker

https://github.com/RenderToolbox/VirtualScenes/wiki/Matlab-on-Docker-and-EC2



### DOCKER-DESKTOP

https://github.com/rogaha/docker-desktop

http://tinylab.org/based-on-ssh-build-docker-xpra-desktop/



### docker-ubuntu-vnc-desktop

http://tinylab.org/docker-desktop-system-based-on-vncserver-novnc/

---

**Quick Start**


Run the docker container and access with port `6080`

```
docker run -p 6080:80 dorowu/ubuntu-desktop-lxde-vnc
```

Browse http://127.0.0.1:6080/

<img src="https://raw.github.com/fcwu/docker-ubuntu-vnc-desktop/master/screenshots/lxde.png?v1" width=700/>

---

**VNC Viewer**


Forward VNC service port 5900 to host by

```
docker run -p 6080:80 -p 5900:5900 dorowu/ubuntu-desktop-lxde-vnc
```

Now, open the vnc viewer and connect to port 5900. If you would like to protect vnc service by password, set environment variable `VNC_PASSWORD`, for example

```
docker run -p 6080:80 -p 5900:5900 -e VNC_PASSWORD=mypassword dorowu/ubuntu-desktop-lxde-vnc
```

A prompt will ask password either in the browser or vnc viewer.

---------------------------

**HTTP Base Authentication**


This image provides base access authentication of HTTP via `HTTP_PASSWORD`

```
docker run -p 6080:80 -e HTTP_PASSWORD=mypassword dorowu/ubuntu-desktop-lxde-vnc
```

--------------------

**SSL**


To connect with SSL, generate self signed SSL certificate first if you don't have it

```
mkdir -p ssl
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout ssl/nginx.key -out ssl/nginx.crt
```

Specify SSL port by `SSL_PORT`, certificate path to `/etc/nginx/ssl`, and forward it to 6081

```
docker run -p 6081:443 -e SSL_PORT=443 -v ${PWD}/ssl:/etc/nginx/ssl dorowu/ubuntu-desktop-lxde-vnc
```

------------------

**Screen Resolution**

The Resolution of virtual desktop adapts browser window size when first connecting the server. You may choose a fixed resolution by passing `RESOLUTION` environment variable, for example

```
docker run -p 6080:80 -e RESOLUTION=1920x1080 dorowu/ubuntu-desktop-lxde-vnc
```
--------------------

**Default Desktop User**


The default user is `root`. You may change the user and password respectively by `USER` and `PASSWORD` environment variable, for example,

```
docker run -p 6080:80 -e USER=doro -e PASSWORD=password dorowu/ubuntu-desktop-lxde-vnc
```

-------------------

**Sound (Preview version and Linux only)**

It only works in Linux. 

First of all, insert kernel module `snd-aloop` and specify `2` as the index of sound loop device

```
sudo modprobe snd-aloop index=2
```

Start the container

```
docker run -it --rm -p 6080:80 --device /dev/snd -e ALSADEV=hw:2,0 dorowu/ubuntu-desktop-lxde-vnc
```

where `--device /dev/snd -e ALSADEV=hw:2,0` means to grant sound device to container and set basic ASLA config to use card 2.

Launch a browser with URL http://127.0.0.1:6080/#/?video, where `video` means to start with video mode. Now you can start Chromium in start menu (Internet -> Chromium Web Browser Sound) and try to play some video.

Following is the screen capture of these operations. Turn on your sound at the end of video!

[![demo video](http://img.youtube.com/vi/Kv9FGClP1-k/0.jpg)](http://www.youtube.com/watch?v=Kv9FGClP1-k)






https://linuxhint.com/how-to-install-opencv-on-ubuntu/