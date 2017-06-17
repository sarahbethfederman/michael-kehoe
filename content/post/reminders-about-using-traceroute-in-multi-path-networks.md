+++
author = ""
date = "2017-02-05T11:49:39-08:00"
title = "Reminders about using traceroute in multi-path networks"
author = "mkehoe"
tags = []
image = "img/main/cover2.jpg"
draft = false
comments = true     # set false to hide Disqus comments
share = true        # set false to hide share buttons
menu = ""           # set "main" to add this content to the main menu
+++
### Introduction

First off, I would like to give a plug for [this](https://www.nanog.org/meetings/nanog45/presentations/Sunday/RAS_traceroute_N45.pdf) presentation about how to use/ interpret traceroute.

Traceroute was written before the times of MPLS, ECMP and Clos network designs. Since the rise of those technologies/ topologies, the way that engineers troubleshoot latency/ packet-loss hasn’t really evolved.

If you look at companies like Google/ Facebook/ LinkedIn, they all run Clos topologies within their production datacenters. So what does mean to engineers troubleshooting production issues?

Firstly, the number of paths from *Host A* to *Host B* is usually going to be \> 1\. This means [MTR](https://en.wikipedia.org/wiki/MTR_(software)) (and some default uses of [traceroute](https://en.wikipedia.org/wiki/Traceroute) are largely obselete.

### Example

Systems engineer A complains about higher latency from his application (spread across the datacenter) to the Oracle database that his application uses. Systems engineer B also complains that his (different) application is seeing higher latency to a different Oracle database (which are located in the same segment of the network).

The go-to troubleshooting step here is to ask the DBA to verify if they are seeing higher execution times on the database which correlates in the percieved rise in latency. In this case, the DBA says there is no issue.

The systems engineers then go to the network engineers and ask for help diagnosing the issue, confident that it isn’t an application-level issue. The network engineers ask for a traceroute and an [mtr](https://en.wikipedia.org/wiki/MTR_(software)) print-out. This would be perfect in an older-style network topology, but is not good for Clos style networks. In this particular case, there is ~20 distinct paths between *Host A* (application) and *Host B *(database). In a best case scenario, traceroute might show you 2-3 paths (by default), mtr will only show you one (the first one it discovers). The chances of you finding the bad path is unlikely.

### What to do next?

Linux traceroute (with a few arguments) can actually help you here. traceroute allows you to send multiple queries to help discover all the interfaces you’d be routed through and potentially see interfaces with packet-loss or higher latency.

e.g.

`[root@hostA ~]$ traceroute -q 10 hostB`

This may not discover all paths, but it is a start. Ofcourse you can run it multiple times to build a bigger picture of the network topology.

### Tools

* Facebook wrote [this](https://code.facebook.com/posts/1534350660228025/netnorad-troubleshooting-networks-via-end-to-end-probing/) great article on troubleshooting networks and released [fbtracert](https://github.com/facebook/fbtracert) which is designed to fix this exact problem.
* [Paris Traceroute](https://paris-traceroute.net/) is another open-source tool aiming to address this space. I haven’t used it, so I cannot vouch for its usefulness.