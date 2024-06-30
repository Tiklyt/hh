---
title: Using MPTCP on Windows
layout: default
nav_order: 3
---

# Using MPTCP on Windows

## Using MPTCP on application of your choice
The MPTCP proxy is a **SOCKS5** proxy and runs at **127.0.0.1** on port **1080**,  you can therefore put this address to use MPTCP on the application of your choice.

for example I decided to use the MPTCP on Firefox as shown here :
![installer](./assets/firefox_proxy.png)

and we can verify if Firefox is really using MPTCP when going to : `http://test.multipath-tcp.org/` , this is the website that allow to check if MPTCP is used.

and as we can see, MPTCP is Enabled :
![installer](./assets/mptcp_enabled_firefox.png)

## Using MPTCP on all application
If u want to use MPTCP in all of your application, you can directly our **Proxifier** application that is pre-installed when installing MPTCP Enabler. that will allow you the redirect all the network traffic.

![installer](./assets/proxifier.png)

The button **proxify all traffic button** will proxify all the network traffic onto the the MPTCP proxy.

The button **force IPV4** force the usage of IPV4 on Windows, the machine need to be restarted in order, the change to take effect.