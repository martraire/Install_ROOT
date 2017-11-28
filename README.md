# How to install ROOT on Ubuntu 16.04

A modular scientific software framework. It provides all the functionalities needed to deal with big data processing, statistical analysis, 
visualisation and storage. It is mainly written in C++ but integrated with other languages such as Python and R.

This note is a step by step guide to install ROOT 6.04 in a newly-install 32-bit Ubuntu 16.04. 

For more information, the ROOT official website is at https://root.cern.ch/. The ROOT installation guide is very helpful, 
especially if you are using a different operating system: https://root.cern.ch/building-root


## 1. Before installing ROOT, build some prerequisites

The required packages for the installation of ROOT are:

`sudo apt-get install git dpkg-dev cmake g++ gcc binutils libx11-dev libxpm-dev libxft-dev libxext-dev`

Optional packages:

`sudo apt-get install gfortran libssl-dev libpcre3-dev xlibmesa-glu-dev libglew1.5-dev libftgl-dev libmysqlclient-dev libfftw3-dev 
libcfitsio-dev graphviz-dev libavahi-compat-libdnssd-dev libldap2-dev python-dev libxml2-dev libkrb5-dev libgsl0-dev libqt4-dev`

N.B: The page listing the prerequisite packages that need to be installed  to be able to configure and to build basic ROOT is: 
https://root.cern.ch/build-prerequisites. (for different platforms).


## 2. ROOT installation
Here the different steps to install ROOT.

### Get the ROOT source file 
There are two possibilities to get the ROOT source file (v6.04):
- Download ROOT source file on http:/root.cern.ch/drupal/content/downloading-root
- Download with git: `git clone http://root.cern.ch/git/root.git root_src`

### Build ROOT
Create a directory **root-build/** where you are going to build ROOT:
```
mkdir root-build
cd root-build
unset ROOTSYS
cmake -Dall="ON" -Dsoversion="ON" -Dqtgsi="OFF" ../root_src >> cmake.out.txt 2>&1
cmake --build . -- -j4 >> cmake.out.txt 2 > &1
```

### Install ROOT
The installation will be in **/usr/local/root**:
```
cd /usr/local
sudo mkdir root
cd ~/root-build
sudo cmake -DCMAKE_INSTALL_PREFIX=/usr/local/root/ -P cmake_install.cmake
```

Now, you can check the installation:
```
cd /usr/local/root
ls -d */
```

Here, you should see different directories such as: aclocal, bin, cmke, config, emacs, ...

### Run ROOT
The last part is to activate the ROOT environment:
`source /usr/local/root/bin/thisroot.sh`

In order to avoid using this command each time you need ROOT, you can add it in your **.bashrc** :
`source /usr/local/root/bin/thisroot.sh`

