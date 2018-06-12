+++
author = "mkehoe"
categories = ["sre", "interop-itx", "future-of-sre", "publications"]
date = "2018-06-12T13:00:00+00:00"
slug = "the-future-of-reliability-engineering-part1"
title = "Future of Reliability Engineering (Part 1)"
image = "img/main/cover2.jpg"
draft = false
tags = ["sre", "interop-itx", "future-of-sre", "publications"]
comments = false     # set false to hide Disqus comments
share = true        # set false to hide share buttons
menu = ""           # set "main" to add this content to the main menu
+++
Last month at Interop ITX, I gave a presentation on the ‘Future of Reliability Engineering’. I wanted to break down the five new trends that I see emerging in a blog-post series:

Evolution of the Network Engineer (towards Network Reliability Engineers)

**a) Breaking down Silo’s**

The network is no longer a silo. Applications run over the network in a distributed fashion requiring low-latency and large data-pipes. With these requirements, network engineers must understand these requirements, understand how applications are generally deployed for troubleshooting purposes and ensure that they have models to plan for capacity management.

**b) Failure management**

“It’s not a matter of avodiing failure, it’s preparing for what to do when things fail.” Failures are going to happen, the problem is managing them. Theoretically protocols like OSPF, BGP, HSRP give us redundancy, but how does that play in practice. Have you tested it? Equally, a large number of failures in the network come from L1 grey failures. How to you plan to detect and mitigate against these faults?

**c) Testing**

Testing has been an area that network engineering has lacked in forever. In the past 10 or so years, tools like GNS3 have moved the needle. Similarly, as Linux Network Operating Systems become more common, the ability to stage configuration and run regression tests. In the future, we will get to the point where you can run tests of new configuration before it is deployed to production.

**d) Network programmability & Automation**

Over the past few years, network device management has finally evolved (slightly) away from SSH/ Telnet/ SNMP into programmable models where we can get away from copy-pasting configuration everywhere and polling devices to death (literally).

This is not dissimilar from the evolution of server management, where tools like Puppet/ Chef/ CFEngine/ Salt came along and made device management extremely simple and orchestratable. In a number of ways (depending on the organization), this displaced the traditional system administration role.

Coming back to the network again, as the network becomes programmable, the traditional network engineer role will need to evolve to know how to program and orchestrate these systems en-masse. 

**e) Measure everything!**

Long live the days of only having SNMP available to measure network performance. The rise of streaming telemetry, and the use of network agents to validate network performance is a must. Further to that, triaging network issues is generally extremely difficult, so you should have some form of monitoring on most layers of the network L1, L2, L3, L4 and L7\. There should be ways to measure availability of your network

The next post in this series will be on Chaos Engineering.
