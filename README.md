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
Then search for WSL in the Windows Microsoft Store to download Ubuntu 22.04.4 LTS-WSL (You can also choose Debian, etc.)

After the download is complete, install it and set the username and password after installation.

WSL1 is installed successfully

## 2 Install Ubuntu prerequisite software
```bash
sudo apt-get update && sudo apt-get upgrade # Update sources and packages
sudo apt-get install -y gcc cmake build-essential autoconf automake subversion libtool git pkg-config openjdk-11-jdk
```

## 3 Download beagle-lib-3.1.2, openmpi-4.1.5 and mrbayes-3.2.7
