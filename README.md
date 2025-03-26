# bishengorange/Mrbayes-Mpi_in_WSL
Install Mrbayes software running multi-threaded on WSL (Windows Subsystem for Linux)

## Get started
1. WSL1;
2. [beagle-lib-3.1.2](https://github.com/beagle-dev/beagle-lib/archive/refs/tags/v3.1.2.tar.gz);
3. [openmpi-4.1.5](https://download.open-mpi.org/release/open-mpi/v4.1/openmpi-4.1.5.tar.gz);
4. [mrbayes-3.2.7](https://github.com/NBISweden/MrBayes/releases/download/v3.2.7/mrbayes-3.2.7.tar.gz);

## 1 Install Linux on Windows with WSL1
To install WSL1, please take a look at the official tutorial of [WSL](https://learn.microsoft.com/en-us/windows/wsl/install).
Or download WSL distribution in the Windows Microsoft store.

### How to install WSL in the Windows Microsoft Store
First, enable the WSL function, Follow these steps: 

Windows Control Panel -> Programs and Features -> Turn Windows features on or off -> √ Windows Subsystem for Linux -> Restart.

WSL2 is turned on by default and needs to be set to WSL1 in Powershell.

Set the default WSL version to WSL1：
```PowerShell
wsl --set-default-version 1
```
Then search for WSL in the Windows Microsoft Store to download Ubuntu 22.04.4 LTS-WSL (You can also choose Debian, etc.).

After the download is complete, install it and set the username and password after installation.

WSL1 is installed successfully.

## 2 Install Ubuntu prerequisite software
```bash
sudo apt-get update && sudo apt-get upgrade # Update sources and packages
sudo apt-get install -y gcc cmake build-essential autoconf automake subversion libtool git pkg-config openjdk-11-jdk
```

## 3 Download beagle-lib-3.1.2, openmpi-4.1.5 and mrbayes-3.2.7
Download beagle-lib-3.1.2.tar.gz, mrbayes-3.2.7.tar.gz, and openmpi-4.1.5.tar.gz in Releases (Note: I haven’t tried a higher version of beagle. I don’t know if it applies to Mrbayes3.2.7.).

Download and extract beagle-lib-3.1.2.tar.gz, mrbayes-3.2.7.tar.gz, and openmpi-4.1.5.tar.gz to any location in Windows (example path: C:\Mrbayes-Mpi_in_WSL-Package).

Copy beagle-lib-3.1.2.tar.gz, mrbayes-3.2.7.tar.gz, and openmpi-4.1.5.tar.gz to WSL, and then unzip it.
```bash
cp /mnt/d/Mrbayes-Mpi_in_WSL-Package/beagle-lib-3.1.2.tar.gz /home/username/
tar -xzvf beagle-lib-3.1.2.tar.gz

cp /mnt/d/Mrbayes-Mpi_in_WSL-Package/mrbayes-3.2.7.tar.gz /home/username/
tar -xzvf mrbayes-3.2.7.tar.gz

cp /mnt/d/Mrbayes-Mpi_in_WSL-Package/openmpi-4.1.5.tar.gz /home/username/
tar -xzvf openmpi-4.1.5.tar.gz
```
## 4 Install step by step
Installation sequence: beagle-lib-3.1.2 -> openmpi-4.1.5 -> mrbayes-3.2.7.
### 4.1 beagle-lib-3.1.2
```bash
cd
cd beagle-lib-3.1.2 && ll
./autogen.sh
./configure
make
sudo make install
```
Configure environment variables
```bash
vim ~/.bashrc
```
Add the following to the end of the .bashrc file
```bash
export LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH
export PKG_CONFIG_PATH=/usr/local/lib/pkgconfig:$PKG_CONFIG_PATH
```
```bash
source ~/.bashrc
```
### 4.2 openmpi-4.1.5
```bash
cd
cd openmpi-4.1.5 && ll
./configure
make
sudo make install
```
Configure environment variables
```bash
vim ~/.bashrc
```
Add the following to the end of the .bashrc file
```bash
MPI_HOME=/usr/local/openmpi
export PATH=${MPI_HOME}/bin:$PATH
export LD_LIBRARY_PATH=${MPI_HOME}/lib:$LD_LIBRARY_PATH
export MANPATH=${MPI_HOME}/share/man:$MANPATH
```
```bash
source ~/.bashrc
```
Verify installation
```bash
cd examples && ll
make
mpirun -np 4 hello_c
```
### 4.3 mrbayes-3.2.7
```bash
cd
cd mrbayes-3.2.7/ && ll
./configure --with-mpi --with-beagle
make
sudo make install
```
Thus, the installation was successful
## Running multi-threaded Mrbayes
```bash
mpirun -np 4 mb # 4 cores running Mrbayes (number of cores depends on computer CPU)
```
