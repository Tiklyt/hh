---
layout: default
title: Configuration
nav_order: 2
nav_titles: true
titles_max_depth: 2
---

#	 Configuring network interface
Now, we need to configure network interface to choose which interface will be a normal subflow or a backup subflow. MPTCP Enabler can automatically configure these parameter with a pre-generated configuration file.
The configuration file is structured as follow :
```
{
  "ManageKernelLocation": true,
  "ManageEndpoint": true,
  "Config": [
    {
      "InterfaceName": "Realtek PCIe GbE Family Controller",
      "FriendlyInterfaceName": "Ethernet",
      "WindowsMacAddress": "D8-BB-C1-1C-10-F3",
      "LinuxMacAddress": "9A-8C-E8-09-4A-CF",
      "Types": ["subflow"]
    },
    {
      "InterfaceName": "TP-Link Wireless MU-MIMO USB Adapter",
      "FriendlyInterfaceName": "Wi-Fi 2",
      "WindowsMacAddress": "78-8C-B5-B9-11-A2",
      "LinuxMacAddress": "3A-BB-9C-AC-4B-9E",
      "Types": ["subflow","backup"]
    }
  ],
  "Proxy": {
    "proxyAddress": "",
    "proxyPort": "",
    "user": "",
    "password": ""
  },
  "SubflowNr": 2,
  "AddAddrAcceptedNr": 4
}
```

 - **ManageKernelLocation** : this parameter if set to true, MPTCP Enabler will automatically change the kernel location to our pre-built MPTCP enabled Linux kernel.
 - **ManageEndpoint** : this parameter if set to true, will setup each endpoint according to this configuration, meaning that parameter that are put into the "Types" section of the configuration will be used.
 - **Config** : it is a list of information about network interface, such as the corresponding MAC Address of the mirrored wsl interface and the Windows interface. The parameter that need to be filled by the user is the **Type** parameter. this is where you decide to if the network interface will be used as a normal subflow or a backup.
 - **Proxy** : This parameter is used if u want to use the double proxy technique in order to multiple network even if the distant server doesn't have MPTCP enabled nor available.
 - **SubflowNr** This parameter is a number that define the maximum number of subflow that can be established.
 - **AddAddrAcceptedNr** This is a number that define the maximum number of address learned over a MPTCP connection.

In the example below, We have decided to use the Ethernet interface to be used as a normal subflow, and the Wi-Fi as a backup subflow.

Note that in-order to these parameter to take effect, you either have to restart WSL2 completely or you have to restart the mptcp-wsl service by running `sudo systemctl restart mptcp-wsl.service`
