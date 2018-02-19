+++
author = "mkehoe"
date = "2017-05-22T18:44:44-08:00"
draft = false
title = "Monitorama Review Day 1"
slug = "monitorama-review-day-1"
tags = ["conferences", "monitorama"]
image = "img/main/cover2.jpg"
comments = true     # set false to hide Disqus comments
share = true        # set false to hide share buttons
menu = ""           # set "main" to add this content to the main menu
+++

Hi all,

I wanted to write some super rough notes of the various Monitorama talks for those (especially my peers) who weren’t able to attend this year. I’d like to give a shout-out to [Sarah Huffman](https://twitter.com/dangerpudding) who drew notes from the presentations today

Note: You can watch the stream [here](https://www.youtube.com/watch?v=P8dc-rLnLr0)

Note: I’ve done my best to put the key take-aways into each presenters talk (with my own opinions mixed in where noted). If you feel like I’ve made an error in representing your talk, please let me know and I’ll edit it.

**Today’s Schedule:**

* The Tidyverse and the Future of the Monitoring toolchains - John Rauser
* Martyrs on Film: Learning to hate the \#oncallselfie - Alice Goldfuss
* Monitoring in the Enterprise - Bryan Liles
* Yo Dawg: Monitoring Monitoring Sytems at Netflix - Roy Rapoport
* Our Many Monsters - Megan Actil
* Tracing Production Services at Stripe - Aditya Mukerjee
* Linux debugging tools you’ll love - Julia Evans
* Instrumenting SmartTV’s and Smartphones in the Netflix app for modeling the Internet - Guy Cirino
* Monitoring: A Post Mortem - Charity Majors
* The Vasa: Redux - Pete Cheslock

**The Tidyverse and the Future of the Monitoring toolchain - John Rauser**

* [Sarah Huffman Notes](https://twitter.com/dangerpudding/status/866718397337288704/photo/1)
* [R-language](https://www.r-project.org/about.html)
* [Tidyverse](http://tidyverse.org/) - “set of shared principles”
* The ideas in the tidyverse are going to transsform everything having to do with data manipulation and visualization
* [ggplot2](http://ggplot2.org/) - compact and expressive (vs D3 lib) way to draw plots
* Dataframe - Tibble (nested data frame)
  * flexible, uniform data container
* R language - Can pipe datasets and chain operations together
* DPLYR - will displace SQL like languages for data-analytics work.
  * DSL for data manipulation
* How to get started - RStudio
* Goal: Inspire tool makers - programming as a way of thinking
* “Toolmakers should look to the tidyverse for inspiration”

**Martyrs of Film: Learning to hate the \#oncallselfie - Alice Goldfuss **

* [Sarah Huffman Notes](https://twitter.com/dangerpudding/status/866718776208654336/photo/1)
* Benfits of oncall
  * Hones troubleshooting
  * Forces you to identify the weak points in your systems
  * Teaches you what is and isn’t production-ready
  * Team bonding
* Learn to hate the on call selfie - people complained on Twitter I get paged alot (noted via \#oncallselfie)
* We use oncall outages as war-stories - and be hero’s
  * Action scenes stop the plot
* Red flags (from alice’s survey)
  * Too few owning too much
  * Symptoms of larger problems:
    * bumping thresholds
    * snooze pages
    * delays
    * Poor Systems visibility/ Team visibility

* Too many pages
  * 17% of people said 100+ (worst case)
  * 1.1% people got 25-50 (best case)
* How do we get there
  * Cleanup - actionable alerts
    * Something breaks
    * Customers notice
    * I am I the best person to fix it
    * I need to fix it immediately

  * (side note) Cluster alerts - Get 1 alert for 50 servers rather than 50 alerts for 50 servers
* Devs oncall - More obligated to fix issues
* Companies who actively look at oncall numbers
  * Heroic
  * Etsy
  * Github


**Monitorings things at your day job (Monitoring int he enterprise ) - Bryan Liles**

* [Sarah Huffman Notes](https://twitter.com/dangerpudding/status/866754545237475328/photo/1)
* Steps
  * 1\. Pick a tool
  * 2\. Pick another tool
  * 3\. Complain
* How do they know what to monitor
* How do they know when changes happen
* New problem: what should you monitor
* New problem: what should you alert on
* New problem: who should you alert
* New problem: what tools should I use
* New problem: how do you monitor your monitoring tools
* Step back and answer:
  * Jow do you know if your stack works
  * How do you know if your stack works well for others
* SLI - Service level indicator - measurement of some aspect of your service
* SLO - service level objective - target value
* SLA - service level agreement - what level of service have you and your consumers agreed to
* White-box vs black box monitoring
* Black box: Garabage in —\> service —\> garbage out
* White box: service (memory/ cpu/ secret sauce)
* How do you know if you’re meeting SLA’s/ SLO’s?
* Logs
  * Structured log (json logs)
  * Aggregate (send them somewhere centrally)
  * Tell a story
* Metrics
  * One or more numbers give details about something (SLI)
  * Metrics are combined to create time-series
* Tracing:
  * Single activity in your stack touches multiple resources
  * MK Note: Brian is talking on open-tracing at Velocity
* Health endpoints
  * E.g. GET /healthz
  * {“database": “ok", “foo": “ok", “queue\_length” :”ok", "updated at": \<datetime\>}
* do you know what’s going on
  * Logs
  * Metrics
  * Tracing
  * Other things
  * e.g. what happened at 3pm yesterday
  * logs, metrics, tracing, other things paint a picture
* How do we ensure greater visibility:
  * Central point of contact for alerts
  * Research tooling practices for teams
  * What types of monitoring tools do we need
* Philosophies:
  * USE: utilization, saturation and errors
  * RED: Rate, error (date), durations (distribution) - Brendan Gregg
  * Four golden signals: (latency, traffic, errs and saturation) - Google


**Yo Dawg: Monitoring Monitoring systems at Netflix - Roy Rapoport**

* [Sarah Huffman Notes](https://twitter.com/dangerpudding/status/866754565311352832/photo/1)
* A hero’s journey - product development lifecycle
  * This will scale for atleast a month
* Monitoring ain’t alerting
  * Alerting - output’s decisions and opinions
* “everything counts in large amounts”
* “the graph on the wall tells the story….”
* 20-25k alerts a day at netflix
* Have another monitoring system to monitor your monitoring system (Hot/ Cold) watcher
* Question “Is one tv show/ movie responsible for more Netflix Outages” - Alice Goldfish

**Our Many Monsters - Megan Anctil**

* [Sarah Huffman Notes](https://twitter.com/dangerpudding/status/866754576040345600/photo/1)
* Why, metrics, logging, alerting
* Vendor vs Non-vendor
  * Business need
  * Cost!!!!
* vizOps at Slack - 1-5 FTE
* Deep-dive into Slack implementations of:
  * Monitoring: Graphite/ Granfana
  * Logging: ELK
  * Alerting: Icigna
* Cost analysis for above platforms
* Lessons leant

  * Usability - escalation info must be valuable
  * Creation - must be easy
* Key takeway:

  * $$$"Is it worth it”
  * is the time worth it

**Tracing Production Services at Stripe - Aditya Mukerjee**

* [Sarah Huffman Notes](https://twitter.com/dangerpudding/status/866817257371860997/photo/1)
* Tracing is about more than HTTP requests
* Venuer - https://veneur.org
* “If you need to look at logs, there’s a gap in your observability tools”
* Metrics - no context
* Logs - hard to aggregate
* Request traces - require planning
* What’s the differennce between metrics/ logs/ tracing (if you squint, it’s hard to tell them apart)
* What if we could have all three, all the time???
* Standard sensor format - Easier to do all three
* Intelligent metric pipelines (before the monitoring applications)

**Linux debugging tools you’ll love - Julia Evans**

* [Sarah Huffman Notes](https://twitter.com/dangerpudding/status/866817513337765888/photo/1)
* [Accompanying Zine](https://jvns.ca/debugging-zine.pdf)
* Starting off: read code, add print statements, know language
* Wizard tools
  * strace
  * tcpdump etc
  * gdb
  * perf
  * ebpf
  * ftrace
* Ask your OS what your progreams are doing
* strace can make your applications run 50x slower
* MK Note: Julia walked though some examples where time/ strace/ tcpdump/ ngrep were all helpful

**Instrumenting SmartTV’s and smartphones in the netflix app for modeling the internet - Guy cirino**

* [Sarah Huffman Notes](https://twitter.com/dangerpudding/status/866817924782186496/photo/1)
* Making the internet fast is slow
  * faster - better networking
  * slower - broader reach/ congestion
* Don’t wait for it, measure it and deal
* Working app \> feature rich app
* We need to know what the internet looks like, without averages
* Logging anti-patterns
* Averages - can’t see the distribution, outliers heavily distort
* Sampling
  * missed data
  * rare events
* RUM data
* Don’t guess what the network is doing - measure it!

**Monitoring: A Post Mortem - Charity Majors**

* [Sarah Huffman Notes](https://twitter.com/dangerpudding/status/866818886515032066/photo/1)

**The Vasa: Redux - Pete Cheslock**

* [Sarah Huffman Notes](https://twitter.com/dangerpudding/status/866819239218249729/photo/1)

**Sponsor talks (only calling out what I choose to)**

* Netsil
  * Application maps
  * Gives you visibility of your topology
  * Techniques
    * APM
    * Tracking (zipkin)
    * proxies
    * OS tracing (pcap/ ePBF)
  * MK Note: Not sure how this works for encrypted data streams
* Datadog
  * They are hiring
    * Apparently is everyone else
  * What do you look for
    * Knowledge
    * Tools
    * Experience
  * Suggestions
    * Knowledge
      * Write blog peices
      * Meetups (Knowledge)
    * Tools
      * Open source
      * studentpack.datadoghq.com
    * Experience
      * Internships
    * Share your knowledge
    * Share your tools
      * share your experience
