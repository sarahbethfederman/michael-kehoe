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

1\. You are not exposing this server to the public internet.

2\. You are running several NTP servers within your network to keep it highly-available. Tip: Using Anycast is a good way to create a highly-available set of NTP servers for a larger-sized network.

3\. You are running a central set of time servers for your network. Every host should not be using external time servers.

3\. If you **really** need very accurate time, do not run NTP servers on Virtual Machines or Containers.

### Installation

Debian based systems:

`apt-get install ntp`

Linux based systems:

`yum install ntp`

### Configuration

{% gist 3671aefc504de4895a151532025ff680 %}

### Automation

I strongly suggest you use some type of configuration management system to manage ntp configuration over a fleet of systems.

I recomment:

*   Puppet - [puppetlabs-ntp](https://github.com/puppetlabs/puppetlabs-ntp)