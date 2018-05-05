sudo apt install libboost-all-dev -y

/usr/bin/x86_64-linux-gnu-ld: cannot find -lboost_filesystem                                                                                                                                                   
/usr/bin/x86_64-linux-gnu-ld: cannot find -lboost_system                                                                                                                                                         
/usr/bin/x86_64-linux-gnu-ld: cannot find -lboost_thread                                                                                                                                                          
/usr/bin/x86_64-linux-gnu-ld: cannot find -lhdf5_hl                                                                                                                                                                
/usr/bin/x86_64-linux-gnu-ld: cannot find -lhdf5



ln -s /usr/lib/x86_64-linux-gnu/libboost_system.so.1.65.1 libboost_system.so
ln -s /usr/lib/x86_64-linux-gnu/libboost_filesystem.so.1.65.1 boost_filesystem.so
ln -s /usr/lib/x86_64-linux-gnu/libboost_thread.so.1.65.1 libboost_thread.so


# Install Boost from source on Ubuntu
http://www.cnblogs.com/zhcncn/p/3950477.html
http://blog.ovidiuparvu.com/how-to-install-boost-on-ubuntu-pc/
https://www.cnblogs.com/darkknightzh/p/5797940.html
``` sh?linenums
#!/bin/bash
 
###########################################################
#
#
# Boost C++ libraries setup
#
#
###########################################################
 
# Starting setup of Boost 1.55
echo "Setting up Boost 1.55..."
 
 
#----------------------------------------------------------
# Installing dependent packages
#----------------------------------------------------------

sudo apt-get -y install build-essential libicu-dev
 
 
#----------------------------------------------------------
# Installing Boost
#----------------------------------------------------------
  
# Constant values definitions

BOOST_VERSION=1.67.0
BOOST_NAME=boost_${BOOST_VERSION//./_}
FOLDER_NAME=boost-${BOOST_VERSION}
INSTALL_PREFIX=~/Workbench/App/usr/${FOLDER_NAME}
 
# Create a new folder for storing the source code
mkdir ${FOLDER_NAME}
 
# Change directory
cd ${FOLDER_NAME}
 
# Download source code
wget https://dl.bintray.com/boostorg/release/${BOOST_VERSION}/source/${BOOST_NAME}.zip
 
# Extract archive
unzip ${BOOST_NAME}.zip
 
# Change directory
cd ${BOOST_NAME}
 
# Run the script which prepares Boost's build process
./bootstrap.sh --prefix=${INSTALL_PREFIX} --with-libraries=all
 
# Compile the project
./b2 install
 
# Add the Boost libraries path to the default Ubuntu library search path
sudo /bin/bash -c 'echo "/usr/local/lib" > /etc/ld.so.conf.d/boost.conf'
 
# Update the default Ubuntu library search paths
sudo ldconfig
 
# Return to the parent directory
cd ../../
 
# Inform user that Boost 1.55 was successfully installed
echo "Boost was successfully installed."
```
