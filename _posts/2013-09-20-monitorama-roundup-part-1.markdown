---
layout: post
title: "Monitorama roundup part 1"
date: 2013-09-20 17:54
comments: true
tags: [monitoring]
---

Over the past two days I've attended the Monitorama conference in Berlin. The conference covers a number of topics in Open Source monitoring, and reflects the cutting edge in techologies and approaches being taken to monitoring today. It also acts as a melting pot of ideas that get used by lots of people to take those ideas further, or act on them within their businesses.

There were a number of ideas that ran throughout many of the talks, which I considered the key take aways from day one:

- **Alert fatigue is a big problem** - Alert less, remove meaningless alerts, alert only on business need and add context to alerts.

- **Everything is an event stream** - metrics, logs, whatever. Treat it all the same (and store it in the same place).

- **The majority of our metrics don't fit standard distribution**, which makes automated anomaly detection hard. So people are looking for models that fit our data to do anomaly detection.

- **Everyone loves airplane stories.** I heard at least five, three of which ended in crashes.

The first day had a single speaker track, here is my personal summary and interpretation of all the talks:


## [Dylan Richard](https://www.twitter.com/dylanr) - Keynote ##

[Video](https://vimeo.com/75176595)

This was an experience talk about the Obama re-election campaign, what they did that worked, what they wished they had etc.

Essentially they used every tool going, and used whatever made sense for the particular area they were looking at. But they weren't able to look carefully about their alerting and were emitting vast numbers of alerts. To deal with this, they leveraged the power users of their applications, who would give feedback about things not working and then they'd dig into the alerts to track down the causes. To improve on that feedback, they also created custom dashboards for those power users so they could report more context with the problem they were experiencing.

Alert fatigue was mentioned - "Be careful about crying wolf with alerts" because obviously people turn off if there's too much alerting noise, and subsequently "Monitoring is useless without being watched".



## [Danese Cooper](https://www.twitter.com/divedanese) - Open Source Past Future ##

[Video](https://vimeo.com/75179551)

Gave a presentation about the history of open source, where it stands today, and advocated participation in open source and the institutions in that space.


## [Abe Stanway](https://www.twitter.com/abestanway), Etsy - Anomaly Detection with Algorithms ##

[Slides](https://speakerdeck.com/astanway/mom-my-algorithms-suck) | [Video](https://vimeo.com/75183236)

Abe gave a great talk on the history of Statistical Process Analysis and how it is used in quality control on production lines and similar industrial settings. This is all about anomaly detection by looking for events that fall outside three standard deviations from the mean. But unfortunately this detection process only works on normally distributed data, and almost none of the data we collect is normally distributed. He followed this with a number of ideas for approaches to take to describe our data in an automated fashion - and then called on the audience to get involved in helping develop these models.

He also gave an interesting comparison between current monitoring being able to provide us with either a noisy situational awareness, or more limited feedback using predefined directives.


## [Mark McGranaghan](https://twitter.com/mmcgrana), Heroku - Fewer Better Systems ##

[Slides](https://speakerdeck.com/monitorama/berlin-2013-session-mark-mcgranaghan) | [Video](https://vimeo.com/75189473)

Presented the argument that the best systems are the ones that are used constantly - for example failover secondaries often do not work because they have not been subjected to live running conditions and the associated maintenance. So he suggested a bunch of things that are done differently now, which could be done the same, so we get better at doing less things:

- Metrics, Logs & Events - can all be considered events, so make them the same format as events 
- Metric Collection & Alerting - often collect the same data - collect once, and alert from your stored metrics
- Integration testing and QOS monitoring - share a lot of same goals, so do them the same
- Unlike results, errors get specific code for dealing with them - instead treat them as a result but send data that presents the error


## [Katherine Daniels](https://twitter.com/beerops), Gamechanger - Staring at Graphs as-a-Service ##

[Slides](https://speakerdeck.com/monitorama/berlin-2013-session-katherine-daniels) | [Video](https://vimeo.com/75190339)

Gave a great practical talk about how monitoring systems fail, and the series of small decisions that get made to improve individual situations but make the whole system, and the operator's experience, much much worse. Essentially, everything that create monitoring systems with screens full of red alerts, that have been that way for a long time and with no sign of resolution.

As a way forward, she suggested the following:

- Only monitor the key components of your business - remove all the crap
- Find out what critical means to you - understand your priorities
- Fix the infrastructure - start with a zero error baseline
- Plan for monitoring earlier in the development cycle (aka devops ftw)


## [Lindsay Holmwood](https://twitter.com/auxesis), Psychology of Alert Design ##

[Slides](https://speakerdeck.com/auxesis/the-psychology-of-alert-design) | [Video](https://vimeo.com/75321812)

Lindsay presented a number of stories, from air disasters and hospitals, to present two key ideas when designing alerts:

- Don't startle or overload the operator (reduce notifications)
- Don't suggest, expose (provide more context - give relevant situational data at the same time)


## [Theo Schlossnagle](https://twitter.com/postwait) - Monitoring what the hell? ##

[Slides](https://speakerdeck.com/monitorama/berlin-2013-session-theo-schlossnagle) | [Video](https://vimeo.com/75428402)

This talk covered a lot of ground quite quickly, so these were the key things I took away:

- Monitor for failure by reviewing problems that you've identified before, create detailed descriptions of those events, and only them alert on those descriptions - so that you have enough context to provide with an alert so that it's meaningful and actionable to the receiver.
- Alert on your business concerns
- Store all your data in the same place - treat logs, events and metrics the same
- Our data isn't normally distributed and that makes shit hard. The next leaps in dealing with this data will come from outside Computer Science - more likely to be the hard science disciplines.


## [Michael Panchenko](https://twitter.com/mihasya) - Monitoring not just for numbers ##

[Slides](https://speakerdeck.com/monitorama/berlin-2013-session-mikhail-panchenko) | [Video](https://vimeo.com/75319951)

Most of this talk was about the problems of configuration drift, and how subtle differences of systems outside configuration management policy scope can yield big surprises. 

Michael presented his dream of enhancing numerical monitoring with non-numerical and non-binary observations, with some suggestions:

- Monitoring of infrastructure state
- Providing an audit trail of categorical data
- Bring able to compare states across nodes and time

He also suggested describing activity in a standardised context: who, what, when.


## [Jarkko Laine](https://twitter.com/jarkko) - Let your data tell a Story ##

[Slides](https://speakerdeck.com/monitorama/berlin-2013-session-jarkko-laine) | [Blog](http://bearmetal.eu/theden/let-your-data-tell-a-story/) | [Video](https://vimeo.com/75318590)

This was a really interesting talk about how humans process ideas and information, how these lead to biases in analysis - and how to exploit them.

The talk was an exposition of two main ideas:

- Attention and Memory are limited
- Tell stories to engage the audience

This was condensed to two key directives for dashboard design and using visualisations as a tool for communication:

- Minimise eye fixations
- Maximise data-ink ratio


## [Ryan Smith](https://twitter.com/ryandotsmith) - Predictable Failure ##

[Slides](https://speakerdeck.com/monitorama/berlin-2013-session-ryan-smith) | [Video](https://vimeo.com/75304752)

This talk featured the best airplane (near-) disaster stories as Ryan was extremely enthusiastic about the content. These provided  pertinent links to understanding failure in IT environments.

The most important was learning about failure modes form other users - official documentation will lack in this respect, so you need to hear the war stories from your peers

He also described a bunch of other failure cases, particular related around redundancy and the complexity that ensues.


## Daniele De Matteis & [Harry Wincup](https://twitter.com/harrywincup), Server Density - Monitoring, graphs and visualisations ##

[Video](https://vimeo.com/75484249)

This was a presentation from the designer's perspective on the theory of how visualisations should be presented, based on the experience of creating the new Server Density interface.

They outlined various design principles they strived for:

  - Consistency
  - Context 
  - Clarity (less is more)
  - Perspective (i.e. vertical alignment for context)
  - Appeal (Pleasant user experience)
    - Consistent graphical elements, white space, horizontal and vertical flows, contrast between elements
  - Control (Let user find next path, but make sure it's only click away)

