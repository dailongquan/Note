

``` sh?linenums
echo 'export PATH="/home/lqdai/Workbench/App/anaconda/bin:$PATH"' >> ~/.bashrc
export PATH="/home/lqdai/Workbench/App/JetBrains/clion-2018.1.2/bin/:$PATH" >> ~/.bashrc
export PATH="/home/lqdai/Workbench/App/JetBrains/pycharm-2018.1.2/bin:$PATH" >> ~/.bashrc
export PATH="/home/lqdai/Workbench/App/cmake-3.10.3/bin:$PATH"
echo 'export PATH="/home/lqdai/Workbench/App/MATLAB/R2018a/bin:$PATH"' >> ~/.bashrc


#gcc找到头文件的路径
echo 'export C_INCLUDE_PATH="$C_INCLUDE_PATH:/home/lqdai/Workbench/App/usr/cuda/include"' >> ~/.bashrc

#g++找到头文件的路径
echo 'export CPLUS_INCLUDE_PATH="$CPLUS_INCLUDE_PATH:/home/lqdai/Workbench/App/usr/cuda/include"' >> ~/.bashrc

#找到动态链接库的路径
echo 'export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/home/lqdai/Workbench/App/usr/cuda/lib64"' >> ~/.bashrc 
 
#找到静态库的路径
echo 'export LIBRARY_PATH="$LIBRARY_PATH:/home/lqdai/Workbench/App/usr/cuda/lib64"' >> ~/.bashrc 
 
source ~/.bashrc  
```
 