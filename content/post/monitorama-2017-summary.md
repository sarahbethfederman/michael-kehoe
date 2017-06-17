+++
author = "mkehoe"
date = "2017-05-26T09:00:00-08:00"
draft = false
title = "Monitorama 2017 Summary"
slug = "monitorama-2017-summary"
tags = ["conferences", "monitorama"]
image = "img/main/cover2.jpg"
comments = true     # set false to hide Disqus comments
share = true        # set false to hide share buttons
menu = ""           # set "main" to add this content to the main menu
+++

The past few days, I’ve been in Portland for the 2017 Monitorama conference. The conference had to literally fail-over between venues Monday night due to a [large power-outage](http://www.opb.org/news/article/portland-oregon-downtown-power-outage-pacific-trimet/) across the city. 

Monitorama brought together a a diverse crowd of engineers and vendors to spend 3 days discussing on call, logging, metrics, tracing and the philosophy of it all.

You can find the schedule [here](http://monitorama.com/#schedule)

And the video’s for each day:

* [Day 1](https://youtu.be/P8dc-rLnLr0)
* [Day 2](https://youtu.be/wnjCNBfH3kg)
* [Day 3](https://www.youtube.com/watch?v=o_8EsyFWal0)

**
**

**Content Summary**

For some reason, there was a large amount of content dedicated to distributed tracing. It was actually a theme that dominated the conference. The amount of of open-source content that was inspired by the original Google Dapper (2010) [paper](https://static.googleusercontent.com/media/research.google.com/en//pubs/archive/36356.pdf) seems to be coming mainstream. 

There was another dominant theme of fixing oncall. This was partially set by Alice Goldfuss’s talk on Day 1 and continued throughout the conference. To be honest, I had no idea how bad some people’s on-call shifts are. I’ve certainly done very well during my time at LinkedIn. It does seem that we need to get smarter about what we alert on.

There was also a number of talks that boiled down to: “This is how my company monitors”. It was definitely interesting to see the use of open-source stack’s at larger companies and a general tendancy to dislike of paying large sums of money to vendors. 

Given my position (and privilege), I’ve been able to learn most of the content during my time at LinkedIn. There were however some talks that I walked away from thinking about how I/ LinkedIn can do a better job. Below are some of my favorite talks (in order of presentation).

**Day 1: The Tidyverse and the Future of the Monitoring Toolchain - John Rauser**

John gave a great overview of the Tidyverse toolset and the power of the R language. The visualizations he used in his presentation definitely inspired my team on how we can present some of our incident data in a more meaningful way. 

**Day 1: Martyrs on Film: Learning to hate the \#oncallselfie - Alice Goldfuss**

Alice gave a very real presentation on the state of on call and how we shouldn’t tolerate it. Cleverly using \#oncallselfie’s on Twitter, she created a narrative on how disruptive oncall can be to our lives and how we shouldn’t tolerate it (for the most part). For anyone who is in a team that gets paged more than 10 times a week, I’d recommend watching.

**Day 1: Linux debugging tools you’ll love - Julia Evans**

Julia ran through a number of great Linux debugging techniques and tools that can be used to find problems in your applications. Definitely a lot of tricks for everyone to pick up. Don’t forget to check out her Zines as well at jvns.ca/zines

**Day 2: Real-time packet analysis at scale - Douglas Creager**

Douglas (from Google) ran through some interesting techniques for troubleshooting a hypothetical music streaming issues via doing packet analysis. Google created a tool called ‘TraceGraph’ which plots the number of packets (by-type)/ window vs time, to show interruptions in data-flow. Unfortunately he didn’t deep-dive into much ‘at-scale’ detail. 

**Day 3: UX Design and Education for Effective Monitoring tools - Amy Nguyen**

Amy deep-dived on how you build a body of work that creates an engaging monitoring tool. She did a great job of highlighting anti-patterns in monitoring tools. She went on to give tips on how you build effective UI’s for monitoring systems. 

**Final words**

Firstly, Kudos to the Monitorama team for running the conference so smoothly given what they had to deal with. Unfortunately, the conference had some competing threads on how you should create a monitoring philosophy which probably didn’t help the smaller companies in attendence. The idea that monitoring is broken is a half-truth at best. We have the best tools we ever have, we just haven’t been able to put a coherent strategy together (this is something I’ll try to blog about next week). My key take-aways are:

1. Provide metrics/ logging/ tracing functionality in frameworks so they are free for developers
2. We need a better way to ingest monitoring data in a sensible/ low-cost manner
3. Need to make it easy to take all of this data and make it explorable/ use-able to everyone. **Also, make it consistent as possible!!!!**
4. Alert sensibly, don’t get paged for something that can wait 12 hours. You should care about how oncall affects your work and your life outside of work
