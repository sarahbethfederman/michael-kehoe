+++
author = "mkehoe"
categories = ["sre", "interop-itx", "future-of-sre", "publications"]
date = "2018-07-09T13:00:00+00:00"
slug = "the-future-of-reliability-engineering-part2"
title = "Future of Reliability Engineering (Part 2)"
image = "img/main/cover2.jpg"
draft = false
tags = ["sre", "interop-itx", "future-of-sre", "publications"]
comments = false     # set false to hide Disqus comments
share = true        # set false to hide share buttons
menu = ""           # set "main" to add this content to the main menu
+++
In early May, I gave a presentation on the ‘Future of Reliability Engineering’. I wanted to break down the five new trends that I see emerging in a blog-post series:

**Blog Post Series:**

* [Evolution of the Network Engineer](https://michael-kehoe.io/post/the-future-of-reliability-engineering-part1/)
* Failure is the new Normal (move towards Chaos-Engineering)
* Automation as a Service
* Cloud is King
* Observe & Measure

**Failure is the new Normal (move towards Chaos-Engineering)**

**a) Breaking down Silo’s**

Let’s be real, software will always have bugs, infrastructure will also eventually fail. This isn’t solely a engineering or operations problem, this is everyones problem 

Chaos-Engineering as a practice is actually a good example of breaking down silo’s. Everyone reading this is probably well versed in this meme about “it’s ops problems now" ([link](http://www.developermemes.com/2013/12/13/worked-fine-dev-ops-problem-now/)).

Chaos Engineering forces that pattern to be broken by requiring developers to be invovled in the process. As a result of your chaos-engineering testing, engineering teams should be fixing weak points in your applications/ infrastructure.

**b) Failure Management**

Chaos-Engineering is a great way to test various processes around “failure”. This goes from engineering training to monitoring and automation, all the way to incident response. 

A continuing chaos-engineering practice should be a continual loop of learning and improvement beyond just the code or infrastructure; it’s also about improving processes. 

**c) Testing**

Chaos-Engineering is obviously a form of testing in itself, but more generally speaking, it should be used as a way to improve your general testing posture.

The feedback loop in a chaos-engineering practice should invovlve engineers writing more resilient code that makes it harder for systems to fail. Ofcourse these fixes also need to be continually tested.

**d) Automation**

As SRE’s, we aim reduce manual toil as much as possible and have tools/ systems to do the work for us; in a reliable, predictable manner. This same principal applies for chaos-engineering particularly because your aim is to break the system. Since you are trying to ‘break' the system, you need to do this in a reliable, repeatable manner. 

If you are going to perform chaos-engineering at all, you should at the very least have a source-controlled script that everyone can find and understand.

**e) Measure Everything**

Within a Chaos Engineering practice, the aim is to alter the normal state of service, observe & measure everything that happens in a controlled environment. Before you perform any chaos-engineering test, you should have a solid understanding of what parts of the system you need to observe, closely observe what changes during the chaos test and write up your observations. Over time, you should be able to tell a story of higher availability/ reliability of the service as the chaos-engineering tests and results improve the software. I would strongly recommend a template similar to [this](https://docs.google.com/document/u/1/d/1hec4i4mp_buLr54Fyu0Kg3GdiUETPDYdzm52k9l03aI/edit?usp=drive_web&ouid=104527119449012814539) to record your findings.

In the next post, we’ll look at ‘Automation as a Service’.
