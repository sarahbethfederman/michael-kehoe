+++
author = "mkehoe"
date = "2018-07-07T20:00:00-08:00"
draft = false
title = "LLDP on Linux"
slug = "lldp-on-linux"
tags = ["lldp", "linux"]
image = "img/main/cover2.jpg"
comments = false     # set false to hide Disqus comments
share = true        # set false to hide share buttons
menu = ""           # set "main" to add this content to the main menu
+++
[Link Layer Discovery Protocol](https://en.wikipedia.org/wiki/Link_Layer_Discovery_Protocol) (LLDP) is an independant IEEE protocol (IEEE 802.1AB) that helps with gathering/ advertising a device's identity, capabilities, and neighbors. LLDP is Layer 2 protocol.

LLDP is usually used on network devices (switches/ routers) to find 'neighbor' (connected) devices, but is equally useful on servers to find details of the switch it's connected to. This is not enabled by default on Linux, but here's a quick guide to get it working.

1. Install the package
```
$ sudo yum install lldp
```

2. Start the daemon
```
$ sudo service lldpd start
```

3. Find your neighbor device
```
$ sudo lldpcli show neighbors
```
