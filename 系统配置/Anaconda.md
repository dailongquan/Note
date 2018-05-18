查看安装了哪些包
conda list 


查看当前存在哪些虚拟环境  
conda env list  


检查更新当前conda
conda update conda

创建python虚拟环境
conda create -n ml-py36 python=3.6

激活虚拟环境
activate ml-py36

安装额外的包
conda install -n your_env_name [package]

关闭虚拟环境
source deactivate

删除虚拟环境
conda remove -n your_env_name(虚拟环境名称) --all

删除环境中的某个包
conda remove --name your_env_name  package_name


pip install numpy scipy matplotlib  