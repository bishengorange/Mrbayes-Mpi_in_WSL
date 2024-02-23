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

### How to install WSL in the Windows Microsoft store
First, enable the WSL function, Follow these steps: 
Windows Control Panel -> Programs and Features -> Turn Windows features on or off -> √ Windows Subsystem for Linux -> Restart.
WSL2 is turned on by default and needs to be set to WSL1 in Powershell.
```powershell
# 设置默认WSL版本
	wsl --set-default-version 1
# wslconfig 查看帮助
	wslconfig
# 查看已经安装的子系统
	wslconfig /list
# 设置默认子系统 <Name> 为分发版名字
	wslconfig /setdefault <Name>
```
