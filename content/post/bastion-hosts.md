+++
author = "mkehoe"
categories = ["security", "ssh", "SRE"]
date = "2018-07-24T13:00:00+00:00"
title = "On Bastion Hosts"
image = "img/main/cover2.jpg"
draft = false
tags = ["security", "ssh", "SRE"]
comments = true     # set false to hide Disqus comments
share = true        # set false to hide share buttons
menu = ""           # set "main" to add this content to the main menu
+++
I was at a meetup the other night and a student mentioned that they were learning about bastion hosts and wanted to learn more. So I thought I would do a deep dive on what they are and why to use them.

### What
>Bastion hosts are instances that sit within your public subnet and are typically accessed using SSH or RDP. Once remote connectivity has been established with the bastion host, it then acts as a 'jump' server, allowing you to use SSH or RDP to log in to other instances.
https://cloudacademy.com/blog/aws-bastion-host-nat-instances-vpc-peering-security/

### Why
Bastion hosts act as a gateway or 'jump' host into a secure network. The servers in the secure network will ONLY accept SSH connections from bastion hosts. This helps limit the number of points where you can SSH into servers from and limit it to a trusted set of hosts. This also significantly helps auditing of SSH connections in the secure network.

Bastion hosts typically have more strigent security postures. This includes more regular patching, more detailed logging and auditing.

## How
Bastion setups are rather quiet simple, here are a few simple steps to set one up
1. Provision a new server(s) that are ONLY dedicated for the purpose of bastion access
2. Install any additional security measures (see the cyberciti reference below for specific recommendations
3. Ensure that all servers in the secure network ONLY accept SSH connections from the bastion server(s)
4. Configure your SSH client to talk to hosts in your private network. Replace the `IdentityFile` and domain-names to suit your network:


```
$ cat ~/.ssh/config
Host *.secure.example.com
  IdentityFile %d/.ssh/keyname.extension
  ProxyCommand ssh bastion.corp.example.com -W %h:%p

Host bastion.corp.example.com
  IdentityFile %d/.ssh/keyname.extension

Host *
  PubkeyAuthentication yes
```

### References
* <https://www.cyberciti.biz/faq/linux-bastion-host/>
* <https://cloudacademy.com/blog/aws-bastion-host-nat-instances-vpc-peering-security/>
* <https://www.sans.org/reading-room/whitepapers/basics/hardening-bastion-hosts-420>
* <https://blog.scottlowe.org/2017/05/26/bastion-hosts-custom-ssh-configs/>
