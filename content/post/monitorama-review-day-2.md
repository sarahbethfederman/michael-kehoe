+++
author = "mkehoe"
date = "2017-05-23T23:44:44-08:00"
draft = false
title = "Monitorama Review Day 2"
slug = "monitorama-review-day-2"
tags = ["conferences", "monitorama"]
image = "img/main/cover2.jpg"
comments = true     # set false to hide Disqus comments
share = true        # set false to hide share buttons
menu = ""           # set "main" to add this content to the main menu
+++

Hi all,

Continuing yesterday’s notes. Last night there was actually a large power outage in downtown Portland which caused us to changes venues today. These notes are somewhat incomplete, I'll try to fix them up in the coming days.

Thanks again to [Sarah Huffman](https://twitter.com/dangerpudding) for her notes.

Video can be found [here](https://www.youtube.com/watch?v=wnjCNBfH3kg)

**Anomalies != Alerts - Betsy Nicols**

* Sarah Huffman [notes](https://twitter.com/dangerpudding/status/867095457532583936/photo/1)
* Now, Pain, Relief, Bonus: Use Case
* Detection & action need to be separated
  * Because they aren’t: Anomalies = Alerts
* Pain
  * 1\. Alert Fatigue
* 1\. Alerts —\> Alert Fatigue
* Alerts = Anomalies
* Anomalies —\> Alert Fatigue
* How many anomalies can we reasonably expect?
  * Step 1\. Population distribution
  * Step 2\. Population Density
  * Step 3\. Compute Anomalies/ Day
* To alert or not to alert
  * decision required for reach anomaly
  * anomalies = TP (true positive) union TN
  * likely \#FP \>\> \#TP
* 2\. Seeking needles
  * Difficult to find a strategy to work out when to alert and when not to
* Relief
  * Basic monitoring pattern
    * Data —\> Engine —\> Alert
  * Basic semantic context
    * Streaming
    * Async
    * Sync
  * Semantic Model (with analytics)
    * Attribute Discovery
      * Build data model using extra attributes
  * Action Policy
    * Works off what data we have and makes a decision
    * Conditions
      * Scope
      * Actions
* Takeaways
  * Best monitoring = Math + context
  * preferred strategy
    * anomalies + context = alerts

**Distributed Tracing: How we got here and wehere we’re going - Ben Sigelman**

* Sarah Huffman [notes](https://twitter.com/dangerpudding/status/867095370592952324/photo/1)
* Why are we here
* Chapter 1: What is the purpose of monitoring
  * must tell stories
  * get to ‘why’ (ASAP)
  * storytelling got a lot harder recently
* One story, N storytellers
  * microservices may be here to stay
  * but they broke our old tools
* transactions are not independent
  * the simple thing
  * basic concurrency
    * async concurrency
* Measuring symptoms
  * metrics model symtoms well
  * measure what the end user actually experiences
  * aside: get raw timing from opentracing instrumentation
  * There is such thing as too many metrics
* Chapter 2: Where
  * Introducing Donut Zone: DaaS
    * Microservice-oriented
    * Use Open tracing
  * Demo of open Trace
  * All sampling must be all/ nothing per transaction
  * Not all latency issues are due to contention
  * A new way to diagnose
    * Infer or assign contention ID’s (mutex’s, db tables, network links)
    * Tag Spans with each contention ID they encounter
    * automated root-cause for contention
  * More demo’s of open trace

**Science! Science Harder: How we reinvented ourselves to be data literate, experiment driven and ship faster - Laura Thomson & Rebecca Weiss**

* Sarah Huffman [notes](https://pbs.twimg.com/media/DAiK0BzXgAEAkfX.jpg)
* Decision-making - without evidence
  * How do you find information about how your releases change the use of the product
* Browser = App? Not quite.
  * Need to test against various OS/ Languages/
* Failure to abstract
  * Build a system to answer questions
* Resulted in different data collection systems (blocklist ping vs telemetry)
  * Working around privacy can be hard
* Unified telemetry:
  * One infrastructure, many types of probes and pings
  * Many type of events
  * Unify mental model
* Transparency:
  * Results must be reproducible as a URL
  * Audit a number all the way down to the code
  * Open science, open methodology
  * Push more data you can
* Experimenting with experiments
  * Update daily on any release channel
  * real sampling
  * flip a preference, install a fature, collect data
  * multiple experiments in flight at once
* Data will shape the web. What kind of web do you want

**Real-time packet analysis at scale - Douglas Creager**

* Sarah Huffman [notes](https://twitter.com/dangerpudding/status/867117784798339072/photo/1)
* 2 Goals:
  * Packet captures are useful
  * You don’t make to make fundemental changes to your monitoring stack
* Example scenario
  * Streaming a song via application
  * You get drops
  * Infer throughput problems
  * Logs aren’t usually enough to help solve the problem
  * In-app RUM can help
  * Need to look at the network itself
  * Flow can sometimes be helpful, but unlikely in this case
  * Need to see inside the connections - Packet capture
  * Don’t need the look at the actual payload
  * Tool at Google - TraceGraph
      * Time vs packets
      * graphs packets (by type) and windows to show problems
  * Ok so the graph visualizes the problem - How do we solve it
  * Looks like we have buffer bloat - can’t fix that problem in ISPs
  * TCPDump to the rescue
  * Google streams packet-captures to a central server for processing

**Instrumenting The Rest Of the Company: Hunting for Useful Metrics - Eric Sigler**

* Sarah Huffman’s [notes](https://pbs.twimg.com/media/DAifs4mXsAA6ocr.jpg)
* We have problem $foo, we are going to do $bar
* What data did you use to understand $foo? And how will you know if $bar improved anything
* “Without data, you’re just another person with an opinion”
* Example: We have a chatbot to do everything that we don’t understand
* Takeaway:
  * Look for ways to reverse engineer existing metrics
  * Useful metrics are everywhere. You aren’t alone in digging for metrics. Existing tools can be repurposed

**Whispers in the Chaos: Monitoring Weak Signals - J Paul Reed**

**Monitoring @ CERN - Pedro Andrade**

* Sarah Huffman’s [notes](https://pbs.twimg.com/media/DAjDgTfWAAMlpxI.jpg)
* Introduction to CERN
* 40GB data/s x 4 to collect during testing
* Where is the data stored:
  * Main site
  * Extension site (with 3x100Gb/s link) - Budapest
  * use standard commodity software/ hardware
  * 14k servers, 200k cores
  * 190PB data stored
* Pedro’s team provides monitoring for the data storage/ computation
* Use Open Source tools
  * Collectd
  * Kafka as transport
  * Spark for processing
  * HDFS long term storage
  * Some data in ES/ InfluxDB
  * Kibana/ Grafana for visualizing
  * openstack VM’s - All monitoring services run on this
  * Config done with Puppet


**I volunteer as Tribute: The future of Oncall: Bridget Kromohout**

* Sarah Huffman’s [notes](https://twitter.com/dangerpudding/status/867158388475543552/photo/1)
* How many people dread phone ringing
* Change is the only constant
