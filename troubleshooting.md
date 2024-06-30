---
layout: default
title: Troubleshooting
nav_order: 4
nav_titles: true
titles_max_depth: 2
---

## Troubleshooting
This sections help you troubleshoot any problem during the installation or the usage of MPTCP Enabler and provide a step-by-step guide to check if everything is installed correctly.

## Windows side installation check
Like we said in the home page, .NET 7.0 Desktop Runtime need to be installed in order to run the application.
Also if Hyper-V is not enabled or WSL2, the installer should propose to you to enable Hyper-V or WSL2.
### Installation Folder
To check if the software was correctly installed, check if the folder : `C:\Program Files (x86)\MPTCP\MPTCP Enabler`exist with the following file :
 - BzImage : the linux kernel with MPTCP enabled
 - mptcp_enabler.exe : the service that will attach all network interface into WSL2
 - Proxifier.exe : the application that will allow to proxify all the network traffic into a MPTCP proxy
 - uninstall.sh : the script that is used by Uninstaller.exe to uninstall all services of MTCP Enabler on WSL2.
 - Uninstaller.exe : the application that serve as uninstaller to delete the application.
### Configuration Folder
The configuration folder should be created on `C:\Users\braro\AppData\Local\MPTCP`
this folder should contains the files :
 - **config.json** : the MPTCP Enabler configuration file
 - **log.txt** : the logging file for the MPTCP Enabler, any error should be displayed here

### WSL Configuration file
Normally, when MPTCP Enabler is installed, it should specify the MPTCP enabled Linux kernel path into the WSL configuration file **.wslconfig**  and should be as follow:
```
[wsl2]
kernel = C:\\Program Files (x86)\\MPTCP\\MPTCP Enabler\\bzImage
```

## WSL Side installation check
To check that the MPTCP enabler services installed on WSL, check the presence of the MPTCP service :
 - `/usr/local/bin/mptcp/mptcp-wsl.sh` : the script that run the MPTCP proxy
 - `/etc/systemd/system/mptcp-wsl.service`: the service that run the mptcp-wsl.sh at start of WSL2
  
  Then to check if the service is running , run the command :
  ```bash
sudo systemctl status mptcp-wsl.service
```

it should output that the service is running like this :
```
● mptcp-wsl.service - The Windows MPTCP Enabler Service
     Loaded: loaded (/etc/systemd/system/mptcp-wsl.service; enabled; vendor preset: enabled)
     Active: active (running) since Tue 2024-05-21 10:51:38 CEST; 1h 24min ago
```
  Also the mptcp-wsl service use mptcpize,redsocks, proxychains and microsocks, so to check if these program are installed run the following command :
  - `which mptcpize`
 - `which redsocks`
 - `which proxychains`
 - `which microsocks`

it shoud output :
```
/usr/bin/mptcpize
/usr/sbin/redsocks
/usr/bin/proxychains
/usr/bin/microsocks
```