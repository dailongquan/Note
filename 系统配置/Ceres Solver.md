#CMake

	sudo apt-get install cmake -y

#google-glog + gflags

	sudo apt-get install libgoogle-glog-dev  -y

#BLAS & LAPACK
	sudo apt-get install libatlas-base-dev  -y

#Eigen3
	sudo apt-get install libeigen3-dev  -y

#SuiteSparse and CXSparse (optional)

#If you want to build Ceres as a *static* library (the default)  you can use the SuiteSparse package in the main Ubuntu package repository:

	sudo apt-get install libsuitesparse-dev  -y

#However, if you want to build Ceres as a *shared* library, you must add the following PPA:

	sudo add-apt-repository ppa:bzindovic/suitesparse-bugfix-1319687
	sudo apt-get update
	sudo apt-get install libsuitesparse-dev


	sudo apt install libceres-dev