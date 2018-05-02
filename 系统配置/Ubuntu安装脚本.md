
### 目录相关
echo "lqdai" | sudo -S chmod -R 777 ~/Workbench

echo "lqdai" | sudo -S  mount -o rw -t nfs -o vers=3 192.168.3.14://volume2/Workbench-Z1Z7AQCM-4T/Workbench  ~/Workbench-NAS
echo "lqdai" | sudo -S  mount -o rw -t nfs -o vers=3 192.168.3.14://volume3/Data-ZDH1BLYG-4T   ~/Workbench-NAS/Data
echo "lqdai" | sudo -S mount -o rw -t nfs -o vers=3 192.168.3.14://volume4/Multimedia-ZDH1BMJ0-4T  ~/Workbench-NAS/Multimedia
echo "lqdai" | sudo -S mount -o rw -t nfs -o vers=3 192.168.3.14://volume1/Backup-ZA17H844-8T   ~/Workbench-NAS/Backup
echo "lqdai" | sudo -S mount -t davfs https://dav.jianguoyun.com/dav/Workbench  ~/Workbench-NAS/IO/webdav/jianguoyun/

echo "lqdai" | sudo -S mount -o  loop -t iso9660 xxx.iso  /mnt/iso


### 编译环境
echo "lqdai" | sudo -S apt install build-essential git -y


### SSH & VNC
echo "lqdai" | sudo -S apt install openssh-server x11vnc -y
 
 ### Chrome
echo "lqdai" | sudo -S wget https://repo.fdzh.org/chrome/google-chrome.list -P /etc/apt/sources.list.d/
wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
echo "lqdai" | sudo -S apt update
echo "lqdai" | sudo -S apt install google-chrome-stable -y

### Latex
echo "lqdai" | sudo -S apt install texlive-full texstudio -y

### Webmin
wget -q -O - http://www.webmin.com/jcameron-key.asc | sudo apt-key add  -
echo "lqdai" | sudo -S add-apt-repository "deb http://download.webmin.com/download/repository sarge contrib"
echo "lqdai" | sudo -S apt install apt-transport-https -y
echo "lqdai" | sudo -S apt update
echo "lqdai" | sudo -S apt install webmin -y

### Docer-CE
echo "lqdai" | sudo -S apt install apt-transport-https ca-certificates curl gnupg2 software-properties-common -y
curl -fsSL https://mirrors.tuna.tsinghua.edu.cn/docker-ce/linux/ubuntu/gpg | echo "lqdai" | sudo -S apt-key add -
echo "lqdai" | sudo -S add-apt-repository  "deb [arch=amd64] https://mirrors.tuna.tsinghua.edu.cn/docker-ce/linux/ubuntu $(lsb_release -cs)  stable"
echo "lqdai" | sudo -S apt update
echo "lqdai" | sudo -S apt install docker-ce -y
sudo docker pull registry.docker-cn.com/nvidia/cuda:latest

### Anaconda(注意链接地址)
wget -O anaconda https://repo.anaconda.com/archive/Anaconda3-5.1.0-Linux-x86_64.sh
chmod u+x anaconda
bash anaconda -b -p ~/Workbench/App/anaconda
rm anaconda3

### CUDA(注意链接地址)
wget -O cuda-repo-ubuntu http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1704/x86_64/cuda-repo-ubuntu1704_9.1.85-1_amd64.deb
echo "lqdai" | sudo -S dpkg -i cuda-repo-ubuntu1704_9.1.85-1_amd64.deb
echo "lqdai" | sudo -S apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1704/x86_64/7fa2af80.pub
echo "lqdai" | sudo -S apt update
echo "lqdai" | sudo -S apt install cuda




# Which version of Ubuntu is my Linux Mint installation based on?

You'll find Ubuntu version in the /etc/upstream-release/lsb-release file:

	$ cat /etc/upstream-release/lsb-release
	DISTRIB_ID=Ubuntu
	DISTRIB_RELEASE=14.04
	DISTRIB_CODENAME=trusty
    
To figure out which subrelease you are using, you need to know what kernel you are running, e.g. here kernel 3.19:

	$ uname -r
	3.19.0-32-generic
    
Then you compare it with the [Ubuntu Kernel Support schedule](https://wiki.ubuntu.com/Kernel/LTSEnablementStack) which says that in my case, the 3.19 kernel matches 14.04.3.
    
    sudo apt-get update && sudo apt-get upgrade



## Toolchain test builds

    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
  
  	sudo apt-get install gcc-7 g++-7 gcc-6 g++-6 gcc-4.9  g++-4.9

  	sudo apt-get install build-essential
  
## Uget  
  
    sudo add-apt-repository ppa:plushuang-tw/uget-stable
    sudo apt update
    sudo apt install uget    
    
    
## Grub

	sudo nano /etc/default/grub

	sudo update-grub

    
## .bash_profile

	source ~/.bashrc    
    
## .bashrc

	export PATH="/home/lqdai/Workbench/App/anaconda3/bin:$PATH"
    export PATH="/home/lqdai/Workbench/App/clion-2017.3.4/bin:$PATH"
    export PATH="/home/lqdai/Workbench/App/pycharm-2017.3.4/bin:$PATH"
    export PATH="/home/lqdai/Workbench/App/cmake-3.10.3/bin:$PATH"
    export PATH="/home/lqdai/Workbench/App/MATLAB/R2017b/bin:$PATH"
    

## MKL

	https://software.intel.com/en-us/articles/free-ipsxe-tools-and-libraries

	https://software.intel.com/en-us/articles/installing-intel-free-libs-and-python-apt-repo
	
	
	
	
## GDM自动登录

	sudo nano /etc/gdm/custom.conf

\# Enable automatic login for user  
[daemon]  
AutomaticLogin=lqdai  
AutomaticLoginEnable=True  

## GRUB更新

	sudo nano /etc/default/grub

nomodeset i915.modeset=1

	sudo grub2-mkconfig -o /boot/grub2/grub.cfg
	
	
	
	
[Manjaro](https://manjaro.org/) is a user-friendly Linux distribution based on the independently developed Arch operating system. 

## 系统安装

> sudo pacman-mirrors -c China
>
> sudo pacman -Syu filezilla chromium latte-dock texlive-most texlive-lang texstudio 

## Anaconda

> yaourt -S anaconda

Please run

> source /opt/anaconda/bin/activate root
> source /opt/anaconda/bin/deactivate root

to activate and deactivate the anaconda enviroment.


## Enable packet forwarding

Check the current packet forwarding settings:

	sysctl -a | grep forward

You will note that options exist for controlling forwarding per default, per interface, as well as separate options for IPv4/IPv6 per interface.

Enter this command to temporarily enable packet forwarding at runtime:

	sysctl net.ipv4.ip_forward=1
    
Edit /etc/sysctl.d/30-ipforward.conf to make the previous change persistent after a reboot for all interfaces:

    net.ipv4.ip_forward=1
    net.ipv6.conf.default.forwarding=1
    net.ipv6.conf.all.forwarding=1
    
Afterwards it is advisable to double-check forwarding is enabled as required after a reboot.

## Enable NAT With iptables

Install the iptables package. Use iptables to enable NAT:

    sudo iptables -t nat -A POSTROUTING -o internet0 -j MASQUERADE
    sudo iptables -A FORWARD -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
    sudo iptables -A FORWARD -i net0 -o internet0 -j ACCEPT


## Assigning IP addresses to the client PC(s)



## 系统配置

    sudo mount -o rw -t nfs -o vers=3 192.168.3.14://volume2/Workbench-Z1Z7AQCM-4T/Workbench  ~/Workbench-NAS

    sudo mount -o rw -t nfs -o vers=3 192.168.3.14://volume3/Data-ZDH1BLYG-4T   ~/Workbench-NAS/Data

    sudo mount -o rw -t nfs -o vers=3 192.168.3.14://volume4/Multimedia-ZDH1BMJ0-4T  ~/Workbench-NAS/Multimedia

    sudo mount -o rw -t nfs -o vers=3 192.168.3.14://volume1/Backup-ZA17H844-8T   ~/Workbench-NAS/Backup


## 远程连接

    ssh 192.168.0.2

    ssh -t 192.168.0.2 'x11vnc -display :0 -nopw -forever'

    ssh -t 192.168.3.66 'x11vnc -display :0 -nopw -forever'

    ssh -t 192.168.3.36 'x11vnc -display :0 -nopw -forever' #学校测试电脑

    ssh -t 192.168.3.27 'x11vnc -display :0 -nopw -forever' #学校服务器
