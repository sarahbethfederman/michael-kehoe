+++
author = "mkehoe"
date = "2017-05-26T02:00:00-08:00"
draft = false
title = "Monitorama Review Day 3"
slug = "monitorama-review-day-3"
tags = ["conferences", "monitorama"]
image = "img/main/cover2.jpg"
comments = true     # set false to hide Disqus comments
share = true        # set false to hide share buttons
menu = ""           # set "main" to add this content to the main menu
+++

Hi again,

This is today’s notes for Monitorama Day 3.

Link to the video is [here](https://www.youtube.com/watch?v=o_8EsyFWal0)

Today’s Schedule

* Monitoring in a world where you can’t “fix” most of your systems Errors - Brandon Burton
* UX Design and Education for Effective Monitoring Tools - Amy Nguyen
* Automating Dashboard Displays with ASAP - Kexin Rong
* Monitoring That Cares (The End of User Based Monitoring) - Francois Concil
* Consistency in Monitoring with Microservices at Lyft - Yann Ramin
* Critical to Calm: Debugging Distributed Systems - Ian Bennett
* Managing Logs with a Serverless Cloud - Paul Fisher
* Distributed Tracing at Uber scale: Creating a treasure map for your monitoring data - Yuri Shkuro
* Kubernetes-defined monitoring - Gianluca Borello

**Monitoring in a world where you can’t “fix” most of your systems Errors - Brandon Burton**

* Challenge
  * Git clone failures in Mac environment…was a DNS issue
  * Third party service outages - pipit, rubygems, launchpad PPA’s
  * Stuff changed somewhere…leftpad
* Can’t always look at logs due to privacy concerns
* Lots of security/ privacy challenge
* So where are we:
  * Adding metrics on jobs as trends

**UX Design and Education for Effective Monitoring Tools - Amy Nguyen**

* Recent projects
  * Tracing
  * D3
  * Cache for openTSDB
  * Documentation
* Why should we care about user experience
  * Prevent misunderstandings - not everyone should be an expert at interpreting monitoring data
  * Developer velocity - help people reach conclusions faster
  * Data democracy - you don’t know what questions people want to answer with their own data
* UX and your situation (pyramid)
  * Team
  * Documentation
  * Tools (this talk)
  * UX and your situation
* Sharing what you know
  * Education vs intuition
  * Best practices - Use your expertise to determine the most helpful default behavior
  * Potential pitfalls
* Performance: Low hanging fruit
  * Backend
    * Roll-up data over long time ranges
    * Store latest data in memory (e..g. FB Gorilla paper and Beringei project
    * Add a cache layer
    * 
  * Frontend
    * Don’t reload existing data if user changes time window
    * Prevent the user from requesting the data incessantly
    * Lazy-load graphs
* Designing what your users want
  * Performance
  * exploration
  * Simplicity

**Automating Dashboard Displays with ASAP - Kexin Rong**

* Talk outline
  * motivation
  * observation
  * our research
  * going fast
* Problem: Noisy Dashboards
* How to smooth plots automatically:
  * More informative dashboard visualization
  * Big idea: Smooth your dashboards
  * Why: 38% more accurate, 44% faster response
* What do my dashboards tell me today
* Is plotting raw data always the best idea
* Q: What’s distracting abotu raw data?
  * A: In many cases, spikes dominate the plot
* Q: What smoothing function should we use
  * A: Moving average works
* Contstraint: preserve deviations in plots
  * metric: measure kurtosis of the plot
  * Use: scipy
* ASAP - As smooth as possible - while preserving long-term deviations
* Use ASAP.js library
* Going fast:
  * Q: Finding optimal window size:
  * A: Use grid search
* futuredata.standard.edu/asap

**Monitoring That Cares (The End of User Based Monitoring) - Francois Concil**

* Doesn’t matter what the monitoring system says, the experience is broken for the user
* "There are three types of lies: Lies, damned lies, and service status pages"
* You need to talk about monitoring early in the development cycle
* “The key to not being woken up by monitoring alerts is to fix the cause for alerts” - Somethong on the internet, probably

**Consistency in Monitoring with Microservices at Lyft - Yann Ramin**

* Approches and techniques to avoid production incidents with hundreds of micro services and diverse teams
* What are we trying to solve:
  * when developers are oncall with micro services OR scaling operational mindfulness
* I clicked production deploy and Jenkins went green - Opepertunity to grow operational mindfulness
* No-one setup a pager duty list before going to production
* We need alarms on things! Lets copy and paste them from my last service
* We routinely approach monitoring as operations
* We don’t have the SRE role - we hire people who understand operations
* We have system metrics (CollectD, custom scripts)
* What do we get (with consistency in monitoring)
  * Consistent measurement
  * Consistent visibility
  * Point-to-Point debugging
  * Unified tracing
* Salt module for orchestratration (orca)
  * provisions resources
  * interacts with pagerduty, ensures a PD service is created
  * makes sure there’s an oncall schedule
  * blocks deploys if these are missing
* Dashboards:
  * git monorepo
  * ties in with salt
  * dashboards defined in salt
  * every service gets a default dashboard on deploy!
  * Add extra dashboards via Salt
* Benefits
  * consistent look at feel
  * always got alarms
  * flexibility

**Critical to Calm: Debugging Distributed Systems - Ian Bennett**

* 3bn metrics emitted per minute
* Twitter uses YourKit for profiling
* Peeling the onion - debugging methodology
  * Metrics/ Alerting
  * Tuning
  * Tracing/ Logs
  * Profiling
  * Instrumentation/ Code change
* When to peel
  * make a single change, rinse, repeat
  * avoid the urge to make too many changes
* Performance tips
  * keep your code abstracted
  * fixes should be as isolated as possible
* critical issues, pager angry:
  * don’t panic
  * Gut can be wrong
  * You will get tired
  * You will get frustrated
  * May take days to come to correct fix
* Some examples of troubleshooting

**Managing Logs with a Serverless Cloud - Paul Fisher**

* Monitoring the monolith
  * Logs seems like a good best practice
  * Doesn’t scale well
  * Literally burn money via vendors
  * Move from logs to metrics - you shouldn’t need to log into boxes to debug
* Lyft contrains
  * AWS
  * Avoid vendor lock-in
* Lyft’s logging pipeline
  * Heka on all hosts
  * Kinesis firehouse
  * kibana proxy to auth
  * Elastalert
  * pagerduty
* Detailed walkthrough of pipeline

**Distributed Tracing at Uber scale: Creating a treasure map for your monitoring data - Yuri Shkuro**

* Why
  * Use tracing for dependency tracing
  * Root Cause analysis
  * distibuted transaction monitoring
* Demo
* Adding context propogation (tracing) is hard in existing code-bases
* Solution - Add to frameworks (simple config changes)
* They must want to use your product - or sticks and carrots
* Each organization is different - find the best way to implement it
* measure adoption - trace quality scores
  * ensure requests are being properly traced
* github.com/uber/jaeger

**Kubernetes-defined monitoring - Gianluca Borello**

* Monitoring Kubernetes
  * Best practices
  * ideas
  * proposals
* 4 things that are harder now (with microservices and kubernetes)
  * Getting the data
    * You (dev) should not be invovled in monitoring instrumentation
    * You (dev) should not be involved in producing anything that’s not a custom metric
    * Collect everything
  * making sense of the data
  * troubleshooting
  * people
* A lot of tools we have now are not container-aware
