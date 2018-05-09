``` shell?linenums
version=3.2.1
build_root=/home/lqdai/Workbench/Build/glfw

remote_url=https://github.com/glfw/glfw/archive/${version}.tar.gz
local_url=${build_root}/glfw-${version}.tar.gz

build_dir=${build_root}/build
install_prefix=~/Workbench/App/usr/glfw-${version}

test -d ${build_root} || mkdir -p ${build_root} 
cd ${local_url}
wget -O ${local_url}  ${remote_url}
tar -xzvf ${local_url} -C ${build_root}

test -d ${build_dir} || mkdir -p ${build_dir} 
cd ${build_dir}
echo "lqdai" | sudo -S sudo apt-get build-dep glfw
cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=${install_prefix} ..


```
