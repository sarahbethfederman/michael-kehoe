+++
author = "mkehoe"
categories = ["ntp", "linux", "security"]
date = "2016-12-23T11:19:32-08:00"
description = ""
draft = false
featured = ""
featuredalt = ""
featuredpath = ""
linktitle = ""
title = "Keeping a NTP server secure"
type = "post"

+++
### Introduction

Over the years, bad actors have used the Network Time Protocol (NTP) as a successful DDOS attack vector.

Generally speaking, the cause of these attacks is due to NTP mis-configuration.

This post will look at how to build and configure an NTP server and provide insight to help keep your NTP server safe.

### Assumptions

1\. You are not exposing this server to the public internet

2\. You are running several NTP servers within your network to keep it highly-available. Tip: Using Anycast is a good way to create a highly-available set of NTP servers for a larger-sized network

3\. If you \*\*really\*\* need very accurate time, do not run NTP servers on Virtual Machines or Containers.

4\. You are running a firewall that blocks packets that come from outside the network on UDP port 123

### Installation

Debian based systems:

`apt-get install ntp`

Linux based systems:

`yum install ntp`

### Configuration
This is an example configuration for a Linux Server with upstream time servers and NTP clients connecting to the server from the 192.168.1.0/24 network.
<script src="https://gist.github.com/michael-kehoe/3671aefc504de4895a151532025ff680.js"></script>

iptables rules:

`-A INPUT -s 192.168.1.0/24 -p udp --source-port 123:123 -m state --state ESTABLISHED -j ACCEPT`

`-A OUTPUT -s 0/0 -s 0/0 -p udp --destination-port 123:123 -m state --state NEW,ESTABLISHED -j ACCEPT`

### Automation

I strongly suggest you use some type of configuration management system to manage NTP configuration over a fleet of systems.

I recommend:

* Puppet - [puppetlabs-ntp](https://github.com/puppetlabs/puppetlabs-ntp)

### References
* [https://en.wikipedia.org/wiki/NTP_server_misuse_and_abuse](https://en.wikipedia.org/wiki/NTP_server_misuse_and_abuse)
* [https://en.wikipedia.org/wiki/Network_Time_Protocol#Security_concerns](https://en.wikipedia.org/wiki/Network_Time_Protocol#Security_concerns)
* [https://github.com/puppetlabs/puppetlabs-ntp/](https://github.com/puppetlabs/puppetlabs-ntp/)
* [http://www.team-cymru.org/secure-ntp-template.html](http://www.team-cymru.org/secure-ntp-template.html)
* [http://www.thegeekstuff.com/2014/06/linux-ntp-server-client/](http://www.thegeekstuff.com/2014/06/linux-ntp-server-client/)
* [http://doc.ntp.org/4.1.1/accopt.htm](http://doc.ntp.org/4.1.1/accopt.htm)
* [http://doc.ntp.org/4.1.1/miscopt.htm](http://doc.ntp.org/4.1.1/miscopt.htm)