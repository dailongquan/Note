
# 编译安装
```sh?linenums	
eigen_version='3.3.4'
folder_name=eigen-${eigen_version}
install_prefix=~/Workbench/App/usr/${folder_name}

mkdir ${folder_name}
cd ${folder_name}
wget -O eigen-${eigen_version}.tar.gz  http://bitbucket.org/eigen/eigen/get/${eigen_version}.tar.gz
tar zxf eigen-${eigen_version}.tar.gz
mkdir build
cd build
cmake -D CMAKE_INSTALL_PREFIX=${install_prefix} .. 
make install
```