+++
author = ""
date = "2016-11-04T15:00:00+00:00"
draft = false
title = "Complete guide to iptables implementation"
slug = "complete-guide-to-iptables-implementation"
tags = ["linux", "iptables", " networking", " security"]
comments = true     # set false to hide Disqus comments
share = true        # set false to hide share buttons
menu = ""           # set "main" to add this content to the main menu
+++

I've been wanting to put this article together for some time, a complete guide to implementing iptables on a Linux Server.

Firstly, my assumptions:
* You have a reasonable grasp of Linux and [Iptables](http://www.thegeekstuff.com/2011/01/iptables-fundamentals)
* You want to use Iptables to secure a Linux server

**The Basics**
Iptables has by default three chains for the FILTER table:
* INPUT
* OUTPUT
* FORWARD

In this case, we're going to focus on the INPUT chain (Incoming to firewall. For packets coming to the local server)

**Implementation**


**Automation**
I implement these rules using the puppet-iptables module. The module is regularly updated and has a very large feature-set. 

References:
https://gist.github.com/jirutka/3742890
http://www.cyberciti.biz/tips/linux-iptables-10-how-to-block-common-attack.html


