sudo apt install libboost-dev -y

/usr/bin/x86_64-linux-gnu-ld: cannot find -lboost_filesystem                                                                                                                                                   
/usr/bin/x86_64-linux-gnu-ld: cannot find -lboost_system                                                                                                                                                         
/usr/bin/x86_64-linux-gnu-ld: cannot find -lboost_thread                                                                                                                                                          
/usr/bin/x86_64-linux-gnu-ld: cannot find -lhdf5_hl                                                                                                                                                                
/usr/bin/x86_64-linux-gnu-ld: cannot find -lhdf5



ln -s /usr/lib/x86_64-linux-gnu/libboost_system.so.1.65.1 libboost_filesystem.so
ln -s /usr/lib/x86_64-linux-gnu/libboost_filesystem.so.1.65.1 boost_filesystem.so
ln -s /usr/lib/x86_64-linux-gnu/libboost_thread.1.65.1 libboost_thread.so


