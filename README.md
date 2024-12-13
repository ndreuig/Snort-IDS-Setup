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
git clone https://github.com/snort3/libdaq.git
```
Change into the libdaq directory:
```bash
cd libdaq
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


## Disable Generic and Large Receive Offloads (GRO & LRO) using a Systemd Service

To disable Generic and Large Receive Offloads on network cards, follow the steps outlined below. Disabling these offloads is necessary for accurate packet inspection and analysis.

1. Identify Network Adapter Name

Run the command ```ip a``` to determine the name of your network adapter.

2. Verify Current Offload Settings

Use the command ```sudo ethtool -k <network_adapter_name> | grep receive-offload``` to check the current status of GRO and LRO. Replace ```<network_adapter_name>``` with the actual name of your network adapter.

3. Create a Systemd Service

Create a new file ```/etc/systemd/system/ethtool.service``` using the command ```sudo nano /etc/systemd/system/ethtool.service```. Paste the following configuration into the file:

```bash
[Unit]
Description=Ethtool Configuration for Network Interface

[Service]
Requires=network.target
Type=oneshot
ExecStart=/sbin/ethtool -K <network_adapter_name> gro off
ExecStart=/sbin/ethtool -K <network_adapter_name> lro off

[Install]
WantedBy=multi-user.target
```

Replace ```<network_adapter_name>``` with the actual name of your network adapter.

4. Save and Close the File

Save the file by pressing ```Ctrl + X```, then ```Y```, and finally ```Enter```.

5. Set File Permissions

Set the file permissions using the command ```sudo chmod 644 /etc/systemd/system/ethtool.service```.

6. Reload Systemd Daemon

Reload the systemd daemon to pick up the changes using the command ```sudo systemctl daemon-reload```.

7. Enable and Start the Service

Enable the service by running ```sudo systemctl enable ethtool.service```. Start the service using ```sudo systemctl start ethtool.service```.

8. Verify Service Status

Verify that the service is running and there are no errors using the command ```sudo systemctl status ethtool.service```.

9. Verify Offload Settings

Verify that the offload settings have been applied correctly using the command ```sudo ethtool -k <network_adapter_name> | grep receive-offload```.



## Creating a Custom Rule for Snort to Detect ICMP Traffic

To create a custom rule for Snort to detect ICMP traffic, we will begin by creating a file called local.rules.

1. Create a Directory for Rules
Create a directory to store the rules file:

```bash
sudo mkdir /usr/local/etc/rules
```

2. Create a File for Local Rules

Create a file called ```local.rules``` in the newly created directory:

```bash
sudo nano /usr/local/etc/rules/local.rules
```

3. Create a Basic Alert Rule

In the ```local.rules``` file, add the following basic alert rule:

```bash
alert icmp any any -> any any (msg:"ICMP Detected"; sid:1000001;)
```
This rule tells Snort to alert whenever it detects ICMP traffic. The rule consists of the following components:

  - ```alert```: The type of rule (in this case, an alert). This means that when the rule is triggered, Snort will generate an alert.
  - ```icmp```: The protocol to detect (in this case, ICMP). This specifies that the rule is looking for ICMP traffic.
  - ```any any```: The source address and port (in this case, any address and port). This means that the rule will match any source IP address and any source port.
  - ```->```: The direction of the traffic (in this case, from any source to any destination). This arrow indicates the direction of the traffic flow.
  - ```any any```: The destination address and port (in this case, any address and port). This means that the rule will match any destination IP address and any destination port.
  - ```msg```: The message to output when the rule is triggered (in this case, "ICMP Detected"). This is the message that will be displayed when the rule is triggered.
  - ```sid```: The signature ID (in this case, 1000001). This is a unique identifier for the rule. Note that the signature ID starts at 1000001 because the numbers 0 to 999999 are reserved by Snort itself.

4. Test the Rule

To test the rule, run Snort with the following command:

```bash
snort --daq-dir /usr/local/lib/daq -T -c /usr/local/etc/snort/snort.lua -R /usr/local/etc/rules/local.rules
```

5. Modify the Snort Configuration
 
To modify the Snort configuration to include the ```local.rules``` file, edit the ```snort.lua``` file:

```bash
sudo nano /usr/local/etc/snort/snort.lua
```

Change the ```HOME_NET``` Parameter:

Locate the ```HOME_NET``` configuration line and replace it with your actual ```IP address```.

Example of replacing ```192.168.1.0``` with your IP or network:

```bash
HOME_NET = "YOUR_IP_ADDRESS"  -- Replace YOUR_IP_ADDRESS with your actual IP
```

Add the following line to the file:

```bash
include = "/usr/local/etc/rules/local.rules",
```

This line tells Snort to include the ```local.rules``` file when it starts. The comma at the end of the line is important, as it indicates that this is not the last line in the file.

Save the file and run Snort again without specifying the rules location:

```bash
snort --daq-dir /usr/local/lib/daq -T -c /usr/local/etc/snort/snort.lua -i eth0 -A alert_fast
```




## Configuring Pulled Pork for Snort Rule Management

We can start expanding our rule set by downloading free rules and to do that we will install what is called Pulled Pork which will automatically grab the rules for you.

1. Clone the Pulled Pork repository:
```bash
git clone https://github.com/shirkdog/pulledpork3.git
```
This command will download the Pulled Pork repository to your current directory.

2. Change into the Pulled Pork directory:
```bash
cd ~/snort/pulledpork3
```
Make sure you're in the correct directory before proceeding.

3. Create a new directory for Pulled Pork in /usr/local/bin:
```bash
sudo mkdir /usr/local/bin/pulledpork3
```
This directory will hold the Pulled Pork executable and its dependencies.

4. Copy the Pulled Pork executable to the new directory:
```bash
sudo cp pulledpork.py /usr/local/bin/pulledpork3
```
This command copies the Pulled Pork executable to the new directory.

5. Copy the Pulled Pork library to the new directory:
```bash
sudo cp -r lib/ /usr/local/bin/pulledpork3
```
This command copies the Pulled Pork library to the new directory.

6. Make the Pulled Pork executable executable:
```bash
sudo chmod +x /usr/local/bin/pulledpork3/pulledpork.py
```
This command changes the permissions of the Pulled Pork executable to make it executable.

7. Create a new directory for Pulled Pork configuration files:
```bash
sudo mkdir /usr/local/etc/pulledpork3
```
This directory will hold the Pulled Pork configuration files.

8. Copy the Pulled Pork configuration file to the new directory:

```bash
sudo cp etc/pulledpork.conf /usr/local/etc/pulledpork3/
```
This command copies the Pulled Pork configuration file to the new directory.

After completing these steps, you should have Pulled Pork installed and configured to manage Snort rules.

**Verify Pulled Pork is Running**

To verify that Pulled Pork is running, specify the location of Pulled Pork:

```bash
/usr/local/bin/pulledpork3/pulledpork.py -V
```


## Configuring Pulled Pork
# Configuring PulledPork3 for Snort Rules Management

This guide walks you through modifying the PulledPork3 configuration file and integrating it with Snort rules. Follow these steps carefully to ensure a successful setup.

---

## Step 1: Edit the PulledPork Configuration File

1. Open the PulledPork configuration file with the following command:
   ```bash
   sudo nano /usr/local/etc/pulledpork3/pulledpork.conf
   ```

2. In the configuration file:
   - Locate the `registered_rules` setting and change its value from `false` to `true`.
   ```
   registered_rules=true
   ```

3. Go to Snort’s website:
   - Create and verify your Snort account if you haven't already.
   - On the left-hand side of the dashboard, find the "Oinkcode" (API code).
   - Copy the Oinkcode to use later.

4. Return to the terminal and paste your Oinkcode into the `oinkcode` field of the configuration file.

5. Locate the `blocklist_path` setting and comment it out by placing a `#` at the beginning of the line, as this is not needed:
   ```
   #blocklist_path=/path/to/blocklist
   ```

6. Scroll down to the `snort_path` setting:
   - Uncomment the line by removing the `#` at the beginning.
   - Verify that the path is correctly set to your Snort executable.
   ```
   snort_path=/usr/local/bin/snort
   ```

7. Further down, locate the `local_rules` setting:
   - Uncomment the line.
   - Ensure it points to the directory containing your local rules.
   - Remove the trailing comma and any text following it.
   ```
   local_rules=/usr/local/etc/snort/rules/local.rules
   ```

8. Save and exit the file:
   - Press `Ctrl+O` to save.
   - Press `Ctrl+X` to exit.

---

## Step 2: Create the `so_rules` Directory

1. Navigate to the `/usr/local/etc` directory:
   ```bash
   cd /usr/local/etc/
   ```

2. Verify the directory contents:
   ```bash
   ls
   ```

3. Create a new directory named `so_rules`:
   ```bash
   sudo mkdir so_rules
   ```

---

#### Update PulledPork Script for Snort Rules

1. Access the PulledPork script:
   ```bash
   sudo nano /usr/local/bin/pulledpork3/pulledpork.py
   ```

2. Scroll to the `RULESET_URL_SNORT_REGISTERED` setting:
   - Replace `<VERSION>` with the actual version number obtained from the Snort website.
   - For example, if the version is `31470`, modify the line as follows:
   ```
   RULESET_URL_SNORT_REGISTERED="https://snort.org/downloads/rules/snortrules-snapshot-31470.tar.gz"
   ```

3. Save and exit the file:
   - Press `Ctrl+O` to save.
   - Press `Ctrl+X` to exit.

---

#### Run PulledPork3

Execute the PulledPork3 script to download and configure Snort rules:
```bash
sudo /usr/local/bin/pulledpork3/pulledpork.py -c /usr/local/etc/pulledpork.conf
```

---

By following these steps, you have successfully configured PulledPork3 to manage Snort rules effectively. If you encounter errors, double-check the paths and configurations to ensure accuracy.


#### Update Snort Configuration

1. Open the Snort configuration file:
   ```bash
   sudo nano /usr/local/etc/snort/snort.lua
   ```

2. Search for the `ips` variable:
   - Press `Ctrl+W` and type `ips` to locate it.

3. Update the `include` variable to point to the PulledPork rules:
   ```lua
   include = "/usr/local/etc/rules/pulledpork.rules",
   ```

4. Save and exit the file:
   - Press `Ctrl+O` to save.
   - Press `Ctrl+X` to exit.

---

#### Run Snort

Run Snort with the updated configuration:
```bash
snort --daq-dir /usr/local/lib/daq -T -c /usr/local/etc/snort/snort.lua --plugin-path /usr/local/etc/so_rules/
```

---



