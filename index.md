---
title: Installation
layout: default
nav_order: 1
---

## Introduction
MPTCP Enabler is a software that allows the use of MPTCP (usage of multiple network interfaces) when making TCP connections. To convert the TCP traffic into MPTCP, we use a proxy that will receive the TCP connection and make a MPTCP connection instead. You can either choose to specify our MPTCP proxy in the application of your choice or either, to forward all the network traffic into the MPTCP Proxy.
## Pre-requisite
In-order to install MPTCP Enabler, you must have :
  - .NET Desktop Runtime 7.0
  - Windows 10/11 Pro versions
  - Have WSL 2 Enabled
  - Hyper-V Enabled
  - Ubuntu 22.04+ installed on WSL.

## Installation step
Download the executable here, and start it. and it will run an User Interface like this :

it propose to you to choose on which distribution u want to install the MPTCP Enabler service, where the proxy will be running.

![installer](./assets/installer.png)

Since WSL2, doesn't support IPV6, not all Windows the traffic will be redirected into the proxy because Windows will prefer IPV6 over IPV4, if the button "force IPV4" is checked, it will force Windows to only use IPV4.

Once you selected your preference, you can click the install button and wait for the completion of the installation.

## Installation verification
To check if have been installed correctly, normally, all of your network interface must appear on WSL2.

You can check first if mptcp is enabled :
```bash
sysctl net.mptcp.enabled
```
If the result is 1, it mean that MPTCP is enabled on WSL kernel.

Once the MPTCP you have verified that MPTCP have been enabled, you can check if all of the Windows Network Interface appear by running the command :
```bash
ip addr
```
and it should give a result like that :
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 00:15:5d:91:be:af brd ff:ff:ff:ff:ff:ff
    inet 172.28.20.4/20 brd 172.28.31.255 scope global eth0
       valid_lft forever preferred_lft forever

3: eth1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 3a:bb:9c:ac:4b:9e brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.56/24 brd 192.168.1.255 scope global dynamic noprefixroute eth1
       valid_lft 3594sec preferred_lft 3594sec

4: eth2: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 9a:8c:e8:09:4a:cf brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.48/24 brd 192.168.1.255 scope global dynamic noprefixroute eth2
       valid_lft 1836sec preferred_lft 1836sec
```
You can then test if both network interface are working by running a ping using both interface like this :
```bash
ping -I <interfacename> 8.8.8.8
```
if you get a ping back, it's meaning that network interface interface is working.

Now we can test if the MPTCP have been enabled by contacting a MPTCP distant server by running :
```bash
mptcpize run curl http://test.multipath-tcp.org/
```
and it should give an output like this :
`You are using MPTCP!`

We recommend now that you on the configuration section ; in order to configure each network interface and potential distant proxy.