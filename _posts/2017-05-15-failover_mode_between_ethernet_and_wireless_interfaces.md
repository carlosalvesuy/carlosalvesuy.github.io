---
layout: post
title:  "Failover Mode Between Ethernet and Wireless Interfaces on FreeBSD 11"
date:   2017-05-15 18:29:15 -0300
categories: FreeBSD
author: "Carlos Alves"
comments: true
---

I want to use my laptop at home without worrying about if I'm connected through
wifi or cable and without losing connectivity if I switch between them.
My requirements are quite simple:

* If Ethernet cable is connected, use this connectivity.
* If no Ethernet cable is connected, use wireless.
* Keep the same IP address. even if using DHCP.

With [lagg(4)](http://www.freebsd.org/cgi/man.cgi?query=lagg&sektion=4&manpath=freebsd-release-ports),
it is possible to configure a failover which prefers the Ethernet 
connection, for both performance and security reasons, while maintaining the ability
to transfer data over the wireless connection.

This is achieved by overriding the physical Ethernet interface's MAC address with that of the wireless interface.

In this example, the Ethernet interface, **em0**, is the master and the wireless interface, **wlan0**, is the failover.
The wlan0 device was created from iwn0 wireless interface. First, determine the MAC address of the wireless interface:

```
# ifconfig wlan0 | grep ether | cut -d' ' -f2
00:21:70:da:ae:37
```
You need to add/update the following lines in your `/etc/rc.conf` file.

```
ifconfig_em0="ether 00:21:70:da:ae:37 up"
wlans_iwn0="wlan0"
ifconfig_wlan0="WPA country UY powersave"
cloned_interfaces="lagg0"
ifconfig_lagg0="laggproto failover laggport em0 laggport wlan0 DHCP"
ifconfig_lagg0_ipv6="inet6 accept_rtadv"
```

>NOTE: While it's quite obvious, remember that you need to replace interface names,
>MAC address and country code to match the ones present in your system.


Now you can do `service netif restart`
