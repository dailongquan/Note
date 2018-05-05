
#Ubuntu 官方
	
sudo apt install libceres-dev


```sh?linenums	
# CMake
sudo apt-get install cmake
# google-glog + gflags
sudo apt-get install libgoogle-glog-dev
# BLAS & LAPACK
sudo apt-get install libatlas-base-dev
# Eigen3
sudo apt-get install libeigen3-dev
# SuiteSparse and CXSparse (optional)
# - If you want to build Ceres as a *static* library (the default)
#   you can use the SuiteSparse package in the main Ubuntu package
#   repository:
sudo apt-get install libsuitesparse-dev
# - However, if you want to build Ceres as a *shared* library, you must
#   add the following PPA:
sudo add-apt-repository ppa:bzindovic/suitesparse-bugfix-1319687
sudo apt-get update
sudo apt-get install libsuitesparse-dev
```

We are now ready to build, test, and install Ceres.

```sh?linenums	
ceres_solver_VERSION='1.14.0'
INSTALL_PREFIX=~/Workbench/App/usr/ceres-solver-${ceres_solver_VERSION}
FOLDER_NAME=ceres-solver-${ceres_solver_VERSION}

# Create a new folder for storing the source code
mkdir ${FOLDER_NAME}
 
# Change directory
cd ${FOLDER_NAME}

wget http://ceres-solver.org/ceres-solver-${ceres_solver_VERSION}.tar.gz
tar zxf ceres-solver-${ceres_solver_VERSION}.tar.gz
mkdir build
cd build
cmake ../ceres-solver-${ceres_solver_VERSION}
make -j3
make test
#Optionally install Ceres, it can also be exported using CMake which allows Ceres to be used without requiring installation, see the documentation for the EXPORT_BUILD_DIR option for more information.
make install
```



	