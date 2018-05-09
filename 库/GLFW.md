``` shell?linenums
version=3.2.1
build_dir=/home/lqdai/Workbench/Build/glfw

remote_url=https://github.com/glfw/glfw/archive/${version}.tar.gz
local_url=${build_dir}/glfw-${version}.tar.gz

test -d ${build_dir} || mkdir -p ${build_dir} 
cd ${local_url}
wget -O ${local_url}  ${remote_url}
tar -xzvf ${local_url} -C ${root_dir}

sudo apt-get build-dep glfw
```
