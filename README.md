# Snort IDS Setup

## Update and Upgrade System Packages

Before installing Snort, it's essential to ensure that your system's packages are up-to-date and have the latest security patches. Run the following command to update and upgrade your system's packages:
```bash
sudo apt-get update && sudo apt-get upgrade -y
```
This command updates the package index and upgrades all installed packages to their latest versions, ensuring that your system is stable and secure.

## Create a Directory for Snort

Create a new directory called snort to store the Snort installation files:

```bash
mkdir snort
```
### Verify the Directory Exists

Run the ls command to verify that the snort directory has been created:

```bash
ls
```
This should list the snort directory among the other files and directories in the current directory.

## Install Essential Dependencies

After creating the snort directory, install the essential dependencies required for the project. Note that these dependencies will be installed system-wide, not within the snort directory:

```bash
sudo apt-get install -y build-essential autotools-dev libdumbnet-dev libluajit-5.1-dev libpcap-dev \
zlib1g-dev pkg-config libhwloc-dev cmake liblzma-dev openssl libssl-dev cpputest libsqlite3-dev \
libtool uuid-dev git autoconf bison flex libcmocka-dev libnetfilter-queue-dev libunwind-dev \
libmnl-dev ethtool libjemalloc-dev
```
This command installs a wide range of dependencies, including build tools, networking libraries, compression libraries, cryptography libraries, testing frameworks, database libraries, utility libraries, and LuaJIT.

**Note:** The -y flag is used to automatically answer "yes" to any prompts, so the installation process can complete without requiring manual intervention.

## Install PCRE

Change into the snort directory and download the PCRE source code:

```bash
cd ~/snort
```
```bash
wget https://sourceforge.net/projects/pcre/files/pcre/8.45/pcre-8.45.tar.gz
```

Extract the tarball:

```bash
tar -xzvf pcre-8.45.tar.gz
```

Change into the PCRE source directory:

```bash
cd pcre-8.45
```

Configure the build:

```bash
./configure
```

Build PCRE:

```bash
make
```
Install PCRE:

```bash
sudo make install
```
This will install PCRE on your system.


## Install gperftools

Change into the snort directory and download the gperftools source code:

```bash
cd ~/snort
```
```bash
wget https://github.com/gperftools/gperftools/releases/download/gperftools-2.9.1/gperftools-2.9.1.tar.gz
```

Extract the tarball:

```bash
tar xzvf gperftools-2.9.1.tar.gz
```

Change into the gperftools source directory:

```bash
cd gperftools-2.9.1
```

Configure the build:

```bash
./configure
```

Build gperftools:

```bash
make
```

Install gperftools:

```bash
sudo make install
```

This will install gperftools on your system. gperftools is a collection of performance analysis tools that can be used to optimize the performance of your system.

Note that gperftools is not a required dependency for Hyperscan, but it may be useful for optimizing the performance of your system.

## Install Ragel

Change into the snort directory and download the Ragel source code:

```bash
cd ~/snort
```
```bash
wget http://www.colm.net/files/ragel/ragel-6.10.tar.gz
```

Extract the tarball:

```bash
tar -xzvf ragel-6.10.tar.gz
```

Change into the Ragel source directory:

```bash
cd ragel-6.10
```

Configure the build:

```bash
./configure
```

Build Ragel:

```bash
make
```

Install Ragel:

```bash
sudo make install
```

This will install Ragel on your system. Ragel is a state machine compiler that can be used to generate efficient and flexible state machines.

Note that Ragel is not a required dependency for Hyperscan, but it may be useful for generating state machines that can be used with Hyperscan.

## Download Boost C++ Libraries

Change into the snort directory and download the Boost C++ Libraries source code:

```bash
cd ~/snort
```
```bash
wget https://boostorg.jfrog.io/artifactory/main/release/1.77.0/source/boost_1_77_0.tar.gz
```

Extract the tarball:

```bash
tar -xvzf boost_1_77_0.tar.gz
```
Note that you are not installing the Boost C++ Libraries at this time, but rather just downloading and extracting the source code. The Boost C++ Libraries will be used later in the installation process.

## Install Hyperscan

Change into the snort directory and download the Hyperscan source code:

```bash
cd ~/snort
```
```bash
wget https://github.com/intel/hyperscan/archive/refs/tags/v5.4.2.tar.gz
```

Extract the tarball:

```bash
tar -xvzf v5.4.2.tar.gz
```

Create a new directory for the build process:

```bash
mkdir ~/snort/hyperscan-5.4.2-build
```

Change into the build directory:

```bash
cd hyperscan-5.4.2-build/
```

**Note:** If you don't have CMake installed on your system, you can install it using the following command:

```bash
sudo apt install cmake
```
(depending on your Linux distribution)

**Troubleshooting:** If you encounter an error during the installation process, you may see a message suggesting to run apt --fix-broken install. This is because the package manager (apt) has encountered a broken or incomplete installation.

To resolve this issue, you can run the following command:
```bash
sudo apt --fix-broken install
```
This command will attempt to fix any broken or incomplete installations and resolve any dependencies.

**Note:** CMake will be installed system-wide, so you don't need to specify a specific directory for installation. The installation command will take care of installing CMake in the correct location.

Once CMake is installed, you can proceed with configuring the build.

Configure the build using CMake:

```bash
cmake -DCMAKE_INSTALL_PREFIX=/usr/local -DBOOST_ROOT=~/snort/boost_1_77_0/ ../hyperscan-5.4.2
```

Build Hyperscan:

```bash
make
```

Install Hyperscan:

```bash
sudo make install
```

This will install Hyperscan on your system. Hyperscan is a high-performance regular expression matching library that is used by Snort.

Note that you have already installed the required dependencies for Hyperscan, including PCRE, LuaJIT, and Boost.


**Install Flatbuffers**

Change into the snort directory:

```bash
cd ~/snort
```

Download the Flatbuffers source code:

```bash
wget https://github.com/google/flatbuffers/archive/refs/tags/v2.0.0.tar.gz -O flatbuffers-v2.0.0.tar.gz
```

Extract the tarball:

```bash
tar -xzvf flatbuffers-v2.0.0.tar.gz
```

Create a new directory for the build process:

```bash
mkdir flatbuffers-build
```

Change into the build directory:

```bash
cd flatbuffers-build
```

To resolve this issue, you can run the following command:

```bash
sudo apt --fix-broken install
```

Configure the build using CMake:

```bash
cmake ../flatbuffers-2.0.0
```

Build Flatbuffers:

```bash
make
```

Install Flatbuffers:

```bash
sudo make install
```

This will install Flatbuffers on your system. Flatbuffers is a cross-platform serialization library that is used by Snort.

Note that you have already installed the required dependencies for Flatbuffers.


**Install Data Acquisition (DAQ) from Snort**

Change into the snort directory:

```bash
cd ~/snort
```

Download the DAQ source code:

```bash
wget https://github.com/snort3/libdaq/archive/refs/tags/v3.0.13.tar.gz -O libdaq-3.0.13.tar.gz
```

Extract the tarball:

```bash
tar -xzvf libdaq-3.0.13.tar.gz
```

Change into the DAQ directory:

```bash
cd libdaq-3.0.13
```

Run the bootstrap script to prepare the build environment:

```bash
./bootstrap
```
**Note:** If you encounter any errors after entering ./bootstrap, ensure that you have the necessary development tools and libraries installed on your system, including libtool, autoconf, and automake. You can usually install these via your package manager. For example, on a Debian-based system, you can run:


```bash
sudo apt-get install libtool autoconf automake
```

After installing the required tools, you may need to rerun the bootstrap script:

```bash
./bootstrap
```

Configure the build:

```bash
./configure
```

Build DAQ:

```bash
make
```

Install DAQ:

```bash
sudo make install
```
This will install DAQ on your system. DAQ is a library that provides a unified interface for packet capture and is used by Snort.

## Update shared libraries
```bash
sudo ldconfig
```
This command updates the dynamic linker's cache, ensuring the system can find the newly installed libraries.

## Install Snort 3

Change into the snort directory:
```bash
cd ~/snort
```

Download the Snort 3 source code:
```bash
wget https://github.com/snort3/snort3/archive/refs/tags/3.1.74.0.tar.gz -O snort3-3.1.74.0.tar.gz
```

Extract the tarball:
```bash
tar -xzvf snort3-3.1.74.0.tar.gz
```

Change into the Snort 3 directory:
```bash
cd snort3-3.1.74.0
```
**Install required dependencies**

Before configuring the build, make sure to install the required dependencies. You can do this by running the following command:
```bash
sudo apt-get install -y build-essential libpcap-dev libpcre3-dev libdumbnet-dev zlib1g-dev liblzma-dev openssl libssl-dev libnghttp2-dev libjemalloc-dev
```
This command will install the necessary dependencies for Snort 3.

**Resolve CMake errors**

If you encounter CMake errors during the configuration process, you may need to install additional packages. Here are some common errors and their solutions:

CMake Error: dnet header not found 
```bash
sudo apt-get install libdumbnet-dev
```
CMake Error: FLEX not found 
```bash
sudo apt-get install flex
```
CMake Error: HWLOC library not found 
```bash
sudo apt-get install libhwloc-dev
```
CMake Error: LuaJIT not found 
```bash
sudo apt-get install libluajit-5.1-dev
```
Configure the build:
```bash
./configure_cmake.sh --prefix=/usr/local --enable-jemalloc
```

Change into the build directory:
```bash
cd build
```

Build Snort 3:
```bash
make
```

Install Snort 3:
```bash
sudo make install
```

This will install Snort 3 on your system.
