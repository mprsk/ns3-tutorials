The following are the basic installation steps for ns-3 using ***buid.py*** in Ubuntu 22.04. However, these steps should also work for other versions.
## Installation path
- Always ensure that the installation path does not have any spaces in between. 
- For example, do not use the below installation path. 
>/home/user/5G Simulations/

- The directory name ***5G Simulations*** in the above installation path has space in it.
- To find your current directory in Ubuntu, type `pwd` in the terminal.

## Verifying dependencies
### C++ Compiler:
To verify if a C++ compiler is present run the below command in terminal:

```
g++ -v
```

The output should display the version of g++ installed as below:

>gcc version 9.5.0 (Ubuntu 9.5.0-1ubuntu1~22.04) 

If not displayed, install g++. Refer to the link for [installation steps](https://linuxconfig.org/how-to-install-g-the-c-compiler-on-ubuntu-22-04-lts-jammy-jellyfish-linux).

### Python
Latest versions of ns-3 requires Python Version >=3.6. To check if Python V3 is installed, execute the below command in terminal:

```
python3 -V
```

The output should display the version of python3 installed installed as below:
>Python 3.12.1

If not displayed, install Python V3 using the below command.

```
sudo apt install python3
```

### CMake

CMake of version >=3.13 is required for ns-3. To verify, execute the below command:

```
cmake -version
```

The output should display the version of cmake installed as below:

>cmake version 3.22.1

If not displayed, install Python V3 using the below command.

```
sudo apt install cmake
```

### Make and Ninja

Verify if make and ninja are installed by executing the below commands:

```
make -v
ninja --version
```
If not installed, install using the below commands:

```
sudo apt install make ninja
```
<!--
### Git tool
Verify if git is installed by executing the below command:

```
git --version
```
If not installed, install using the below commands:

```
sudo apt install git
```
-->

## Downloading ns-3 source archive
- For the tutorial, the installation path used is 
```
kiran@kiran:~/Simulators$ pwd
/home/kiran/Simulators
```
- Create a workspace directory and change into to the created directory

```
mkdir ns3-workspace
cd ns3-workspace
```
- Fetch the ns-3 source archive. Here the below command fetches ns-3.41 version. For other versions, use the suitable link. Note that fetching may take some time depending on your internet bandwidth.

```
wget https://www.nsnam.org/release/ns-allinone-3.41.tar.bz2
```

- Extract the source files

```
tar xjf ns-allinone-3.41.tar.bz2
```
After executing this, a new directory ***ns-allinone-3.41***. Change into the directory.

```
cd ns-allinone-3.41
```

## Building ns-3

- To build ns-3, execute the below command:
```
./build.py --enable-examples --enable-tests
```

- The above command builds ns-3 with default examples and tests. As we are starting with ns-3 and will use examples provided by ns-3, it is recommended to enable examples and tests.

- The execution time of the above command will depend on the system configuration. A typical Intel i5 processor with 8 GB RAM typically takes around 10 minutes for execution (this is what I witnessed and may vary).
- After execution is completed, the output should like the following (warnings can be ignored):

```
Modules configured to be built:
antenna                   aodv                      applications              
bridge                    buildings                 config-store              
core                      csma                      csma-layout               
dsdv                      dsr                       energy                    
fd-net-device             flow-monitor              internet                  
internet-apps             lr-wpan                   lte                       
mesh                      mobility                  netanim                   
network                   nix-vector-routing        olsr                      
point-to-point            point-to-point-layout     propagation               
sixlowpan                 spectrum                  stats                     
tap-bridge                test                      topology-read             
traffic-control           uan                       virtual-net-device        
wifi                      wimax                     

Modules that cannot be built:
brite                     click                     mpi                       
openflow                  visualizer                


-- Configuring done
-- Generating done
-- Build files have been written to: /home/kiran/Simulators/ns3-workspace/ns-allinone-3.41/ns-3.41/cmake-cache
Finished executing the following commands:
mkdir cmake-cache
/usr/bin/cmake -S /home/kiran/Simulators/ns3-workspace/ns-allinone-3.41/ns-3.41 -B /home/kiran/Simulators/ns3-workspace/ns-allinone-3.41/ns-3.41/cmake-cache -DCMAKE_BUILD_TYPE=default -DNS3_ASSERT=ON -DNS3_LOG=ON -DNS3_WARNINGS_AS_ERRORS=OFF -DNS3_NATIVE_OPTIMIZATIONS=OFF -DNS3_EXAMPLES=ON -DNS3_TESTS=ON -G Ninja --warn-uninitialized
 =>  /home/kiran/miniconda3/bin/python3 ns3 build
[0/2] Re-checking globbed directories...
[1636/1925] Building CXX object src/wifi/CMakeFiles/libwifi-test.dir/test/wifi-mac-ofdma-test.cc.o
/home/kiran/Simulators/ns3-workspace/ns-allinone-3.41/ns-3.41/src/wifi/test/wifi-mac-ofdma-test.cc: In member function ‘void OfdmaAckSequenceTest::CheckResults(ns3::Time, ns3::Time, uint8_t)’:
/home/kiran/Simulators/ns3-workspace/ns-allinone-3.41/ns-3.41/src/wifi/test/wifi-mac-ofdma-test.cc:711:1: note: variable tracking size limit exceeded with ‘-fvar-tracking-assignments’, retrying without
  711 | OfdmaAckSequenceTest::CheckResults(Time sifs, Time slotTime, uint8_t aifsn)
      | ^~~~~~~~~~~~~~~~~~~~
[1925/1925] Linking CXX executable ../build/examples/wireless/ns3.41-wifi-eht-network-default
Finished executing the following commands:
/usr/bin/cmake --build /home/kiran/Simulators/ns3-workspace/ns-allinone-3.41/ns-3.41/cmake-cache -j 7
Leaving directory `/home/kiran/Simulators/ns3-workspace/ns-allinone-3.41/./ns-3.41'
```

### Testing ns-3 installation
- After installation is successfully completed, check the folders in the installation directory using the below command:
```
kiran@kiran:~/Simulators/ns3-workspace/ns-allinone-3.41$ ls
bake  build.py  constants.py  netanim-3.109  ns-3.41  __pycache__  README.md  util.py
```

- Change the directory into ns-3.41
```
cd ns-3.41
```
- Test the installation by executing the below command
```
./test.py --no-build
```

- After the execution is successfully completed, the output should like below
> 762 of 762 tests passed (762 passed, 0 skipped, 0 failed, 0 crashed, 0 valgrind errors)

### Running a script
- To run the first Hello World script, execute the below command.
```
kiran@kiran:~/Simulators/ns3-workspace/ns-allinone-3.41/ns-3.41$ ./ns3 run hello-simulator
[0/2] Re-checking globbed directories...
ninja: no work to do.
Hello Simulator
```


### References
- https://www.nsnam.org/docs/tutorial/html/getting-started.html#downloading-ns-3-using-bake