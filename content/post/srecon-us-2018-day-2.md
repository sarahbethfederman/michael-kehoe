+++
author = "mkehoe"
date = "2018-03-28T19:00:00-08:00"
draft = false
title = "SRECon Americas 2018 Day 2 Notes"
slug = "srecon-americas-2018-day-2"
tags = ["conferences", "srecon"]
image = "img/main/cover2.jpg"
comments = false     # set false to hide Disqus comments
share = true        # set false to hide share buttons
menu = ""           # set "main" to add this content to the main menu
+++
Day 2 of SRECon started with an introduction from Kurt and Betsy (the Program Chairs) and then three set of plenary’s talks.

The following is a set of notes I put together from the talks I went to today. 

**If you Don’t Know WHere You’re Going, It Doesn’t Matter How Fast You Get There**
_Nicole Forsgren & Jez Humble_
Slides found [here](https://speakerdeck.com/jezhumble/if-you-dont-know-where-youre-going-it-doesnt-matter-how-fast-you-get-there). The talk generally was about strategic planning and measuring your performance/ success. This part of IT is actually very under-valued. 

These Tweets sums up the presentation well:
{{< tweet 979021720274092034 >}}
{{< tweet 979022413185802240 >}}

Some nice points about the mis-use of Velocity and Utilization as Key Performance Indicators (KPI).

**Security and SRE: Natural Force Multipliers**
_Cory Scott_
Slides [here](https://www.slideshare.net/cory_scott/sre-and-security-natural-force-multipliers)

Heirarchy of Needs in SRE:
1. Monitoring & Inciddent Response
2. Postmortem & Analysis
3. Testing & Release Procedures
4. Capacity Planning
5. Product

Problem Statement:
* High Rate of Change
    * Trust but verify
    * Embrace the Error Budget
    * Inject Engineering Discipline
* Testing in Production is the new normal
    * Dark Canaries

Security Challenges are similar to SRE
* Latency & perf impact
* Cascading failure scenarios
* Service Discovery

Security Challenges
* Authentation
* Authorization
* Access Control Logic

Data center technologies can be all controlled with a single web page application.
* Start with a known-good state
* Asset management
* Ensure visibility
* Validate consistently and constantly

Takeaways or Giveaways
* Your data pipeline is your security lifeblood
* Human-in-the-loop is your last resort, not your first option
* All security solutions must be scalable
* Remove single points of security failure like you do for availability
* Assume that an attacker can be anywhere in your system or flow
* Capture and measure meaningful security telemetry


**What it Really Means to Be an Effective Engineer**
_Edmond Lau_
See coleadership.com/srecon
Effort <> Impact
Impact = Hours spent x (impact produced/hours spent)
leverage = impact produced/ hours spent


What are the high-leverage activities for engineers?
* Do the simple thing first
* Effective engineers invest in iteration speed
* Effictive engineers validate their ideas early and often
* What are the best practices for building good infrastructure for relationships
* Effective engineers explicitly design their alliances
* Effective engineers explicitly share their assumptions
* Work hard and get things done
and focus on high-leverage activities
and build infrastructure for their relationships


**The Day the DNS died**
Jeremy Blosser
tinyurl.com/spdnstalk

Impact
* Sending mail
* Application traffic
* Metrics 

Diagnosing blind (without metrics) is difficult!

resolv.conf is fiddly
* Can only use first 3 entries

Diagnosis
* Assymetric DNS packet flow (94% packet loss)

The Cause
* [Undocumented] Connection tracking

Response
* Incident response was functional
* Ability to respond was compromised
* New DNS design required

New Design
* Dedicated VPC for isolation
* Open security groups with ACLs
* Seperate clusters for app/db vs MTA
* Use DNSMasq for local caching

Lessons learnt
* Not all cloud limits are apparent
* Instrument your support services and protect
* It'a always a DNS problem...excpet when it's a firewall problem
* resolf.conf is not agile

**Stable and Accurate Health-Checking of Horizontally-Scaled Services**
_Lorenzo Salno_
See new Fastly paper on load-balancing: Balancing of the edge: transport affinity without network state - NSDI paper

PoP Deployments
* Space and power are at a premium

Architecture:
* Building a smarter load balancer

Methods:
* machine learning - classifier
* signal processing - filter
* control theoery - controller

Design
Multiple stages system
* Denoising - remove noise from input signal
* Anomaly detection - identify misbehaving instance
* Hysteresis filter - stabilize output

Implementation
Host signals go into a filter which makes a decision about global state of host


**Don't Ever Change! Are Imutable Deployments Really Simplier Faster, and Safer?**
_Rob Hirschfelf_
Immutable Patterns
* Baseline + Config
* Live Boot + Config
* Image Deploy

Image creation
* Do the configuration and capture the immage into a portable format
* This sounds like a lot of work and really slow
* Yes, but it's faster, safer and more scalable


**Lessons Learned from Our Main Database Migrations at Facebook**
_Yoshinori Matsunobu_

User Database
* Stores Social Graph
* Massively Sharded
* Low latency
* Automated Operations
* Pure Flash Storage

What is MyRocks
* MySQL on top of RocksDB
* Open Source, distributed from MariaDB and Percona

MyRocks Features
* Clustered Index
* Bloom filter and Column family
* Transactions, including consistency betweenbinlog and RocksDB
* Faster data loading, deletes and replication
* Dynamic Options
* TTL
* Online logical and binary backup


MyRocks pros vs InnoDB
* Much smaller space (half compared to compressed InnoDB)
* Writes are faster
* Much smaller bytes written

MyRocks cons vs InnoDB
* Lack several features
    * No FK, Fulltext index, spactial index
*  Must use Row based binary logging format
* Reads are slower than InnoDB
* Too many tuning options

MyRocks migration - technical challenges
Migration
* Creating MyRocks instances without downtime
* Creating second MyRocks instance without downtime
* Shadow traffic tests
* Promoting new master

InnoDB vs MyRocks, from SRE PoV
* Server is busier because of double density
* Rocksdb is much newer database that changes rapidly
* MyRocks/ RocksDB relies on BufferIO
* For large transactions, COMMIT needs more work than InnoDB
* There are too amny tuning options
* Faster writes means replication slaves lag less often

Issue: Mitigating stalls
* We upgraded kernel to 4.6
* Changed data loading queries (schema changes) to use MyRocks bulk loading feature
* COmmit stalls every few mins --> now nearly zero

Issue: A few deleted rows re-appeared
* Some of our secondary indexes had extra rows
* Turned out to be a bug in RocksDB compactions that in rare cases on heavy deletions, tombstones might now have been handled correctly

Issue: Scanning outbound delete-markers
Counting from one of the empty tables started taking a few minutes

Lesons Learned
* Learn how core components work
    * RocksDB depends on linux more than innodb
    * Understanding how Linux works helps to fix issues faster
* Do not ignore outliers
    * Many of our issues happened on only handful instances


**Leveraging Multiple Regions to Improve Site Reliability: Lessons learnt from Jet.om**
_Andrew Duch_

* Lesson 1: Sorry I missed this
* Lesson 2: Not everything has to be active-active
* Lesson 3: Three is cheaper than two - you waste 50% of you capacity in a active-active model
* Lesson 4: Practie, Practice, Practice
* Lesson 5: Failover Automation needs to scale


Unfortunately I had to skip the final set of sessions this afternoon due to a conflict. From all acounts, the sessions this afternoon were great.

See everyone tomorrow for day 3!
